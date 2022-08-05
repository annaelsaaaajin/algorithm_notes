# 加一
[LeetCode 66. 加一](https://leetcode.cn/problems/plus-one/)

# 解题思路
高精度加法

# Code
- 模拟
```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        unsigned long long res = 0;
        for (auto i : digits)
            res = res * 10 + i;
        
        res ++;

        vector<int> ans;
        while (res)
        {
            ans.push_back(res % 10);
            res /= 10;
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```
- 高精度加法
```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        reverse(digits.begin(), digits.end());
        return add(digits, {1});
    }

    vector<int> add(vector<int> A, vector<int> B)
    {
        vector<int> C;
        int t = 0;
        for (int i = 0; i < A.size() || i < B.size(); i ++)
        {
            if (i < A.size()) t += A[i];
            if (i < B.size()) t += B[i];
            C.push_back(t % 10);
            t /= 10;
        }
        if (t) C.push_back(1);
        reverse(C.begin(), C.end());
        return C;
    }
};
```

```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        reverse(digits.begin(), digits.end());
        int t = 1;
        for (auto& x: digits) {
            t += x;
            x = t % 10;
            t /= 10;
        }
        if (t) digits.push_back(t);

        reverse(digits.begin(), digits.end());

        return digits;
    }
};
```