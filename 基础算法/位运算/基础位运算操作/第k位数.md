# Link
[AcWing 801. 二进制中1的个数](https://www.acwing.com/problem/content/803/)

# 第k位数模板
```cpp
int get_bit(int n, int k)
{
    return n >> k & 1;
}
```

# 算法思路
- 先把 $n$ 移到第 $k$ 位，此时第 $k$ 位变成了最后一位
  `x = n >> k;`
- 再看最后一位是多少
  `x & 1`
  
# Code
```cpp
#include <iostream>
#include <cmath>

using namespace std;

int get_bit(int n, int k)
{
    return n >> k & 1;
}

int main()
{
    int n;
    cin >> n;
    while (n --)
    {
        int x, cnt = 0;
        cin >> x;
        int len = (int)log2(x) + 1; 
        //对数强制转换为int不然会比较慢
        for (int i = len - 1; i >= 0; i --)
            if (get_bit(x, i)) cnt ++;
        cout << cnt << ' ';
    }

    return 0;
}
```