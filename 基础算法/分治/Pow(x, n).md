# Pow(x, n) 
[LeetCode 50. Pow(x, n) ](https://leetcode.cn/problems/powx-n/)

# 分治
```cpp
class Solution {
public:
    double myPow(double x, long long n) {
        if (n == 0) return 1;
        if (n < 0) return 1.0 / myPow(x, -n);
        double temp = myPow(x, n / 2);
        double ans = temp * temp;
        if (n % 2) ans *= x;
        return ans;
    }
};
```

# 快速幂
- 注意 `n` 为 `INT_MIN`时，`abs` 会爆掉 `int`
```cpp
class Solution {
public:
    double myPow(double x, long long n) 
    {
        typedef long long LL;
        bool is_neg = n < 0;
        double res = 1;
        for (LL k = abs((LL)n); k; k >>= 1) // 注意 n 为 INT_MIN时，abs 会爆掉 int
        {
            if (k & 1) res *= x;
            x *= x;
        }
        if (is_neg) res = 1 / res;
        return res;
    }
};
```