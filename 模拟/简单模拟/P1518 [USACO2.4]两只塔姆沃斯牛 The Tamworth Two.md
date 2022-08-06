# 两只塔姆沃斯牛
[P1518 [USACO2.4]两只塔姆沃斯牛 The Tamworth Two](https://www.luogu.com.cn/problem/P1518)
[AcWing 1373. 两只奶牛](https://www.acwing.com/problem/content/1375/)

# 解题思路
模拟
- `move()`
    - 转弯 
    ```cpp
    if (a < 0 || a >= n || b < 0 || b >= m || g[a][b] == '*')
        d = (d + 1) % 4;
    ```
    - 直走
    ```cpp
    else x = a, y = b;
    ```
- 如何判断无解？
  **状态有限，时间无限，意味着必然会陷入循环**
  **当遍历完所有状态后，仍无解，则一定无解**
  - 状态数量
    - 对于一个人 $S(x, y, d)$
      - 长 $10$
      - 宽 $10$
      - 方向 $4$
      - 总 $10 \times 10 \times 4 = 400$  
    - 对于两个人 G(S1, S2) 
      - 总 $400 \times 400 = 160000$
**所以当枚举到 $160001$ 时无解则无解**
```cpp
for (int i = 1; i <= 160001; i ++ )
{
    move(x1, y1, d1);
    move(x2, y2, d2);
    if (x1 == x2 && y1 == y2)
    {
        cout << i << endl;
        return 0;
    }
}
cout << 0 << endl;
```

- PS：如果不会判断状态数量则可以以**题目限时**为依据规定最大搜索次数
```cpp
#include <ctime>

clock_t start,end;
start = clock();

...

end = clock();
cout<<"time = "<< double(end-start) / CLOCKS_PER_SEC;
```

# Code
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>

using namespace std;

const int N = 15;

int n, m;
char g[N][N];
int dx[] = {-1, 0, 1, 0}, dy[] = {0, 1, 0, -1};

void move(int& x, int& y, int& d)
{
    int a = x + dx[d], b = y + dy[d];
    if (a < 0 || a >= n || b < 0 || b >= m || g[a][b] == '*')
        d = (d + 1) % 4;
    else x = a, y = b;
}

int main()
{
    while (cin >> g[n]) n ++ ;
    m = strlen(g[0]);

    int x1, y1, d1 = 0, x2, y2, d2 = 0;
    for (int i = 0; i < n; i ++ )
        for (int j = 0; j < m; j ++ )
            if (g[i][j] == 'F') x1 = i, y1 = j;
            else if (g[i][j] == 'C') x2 = i, y2 = j;

    for (int i = 1; i <= 160001; i ++ )
    {
        move(x1, y1, d1);
        move(x2, y2, d2);
        if (x1 == x2 && y1 == y2)
        {
            cout << i << endl;
            return 0;
        }
    }

    cout << 0 << endl;
    return 0;
}
```