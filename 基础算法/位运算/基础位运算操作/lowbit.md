# Link
[AcWing 801. 二进制中1的个数](https://www.acwing.com/problem/content/803/)

# $lowbit$ 模板
```cpp
int lowbit(int n)
{
    return n & -n;
}
```

# 算法思路
- $lowbit$
  根据计算机负数表示的特点，如一个数字原码是$10001000$，他的负数表示形势是补码，就是反码$+1$，反码是$01110111$，加一则是$01111000$，二者按位与得到了$1000$，就是我们想要的`lowbit()`操作
  - $Eg$ :
    原码 $x$ : $1000~1000$
    反码 $\sim x$ : $0111~0111$
    补码 $-x$ (即反码 $+1$: $~x+1$ ) : $0111~1000$
    $x AND -x$:
    $1000~1000$
    $0111~1000$
    $AND \Rightarrow$
    $0000~1000$ 即 $1000$
- $x$ 能做多少次 $lowbit$ ，就有多少个 $1$

# Code
```cpp
#include <iostream>

using namespace std;

int lowbit(int a)
{
	return a & -a;
	//return a & (~a + 1);
}

int main()
{
	int n;
	scanf("%d", &n);
	while (n --) 
	{
		int x, sum = 0;
		scanf("%d", &x);
		
		while (x)
		{
			x = x - lowbit(x);
			sum++;
		}
		//for (int i = x; i != 0; i -= i & -i) sum ++;
		
		printf("%d ", sum);
	}
	
	return 0;
}
```
