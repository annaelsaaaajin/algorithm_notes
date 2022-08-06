# 和为K的子数组
[LeetCode 560. 和为K的子数组](https://leetcode.cn/problems/subarray-sum-equals-k/)

# 解题思路
**前缀和 + 哈希表查询**

# Code
```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int n = nums.size();
        int res = 0;
        vector<int> s(n + 1);
        for (int i = 1; i <= n; i ++) s[i] = s[i - 1] + nums[i - 1];
        unordered_map<int, int> cnt;
        cnt[0] = 1;
        for (int i = 1; i <= n; i ++) 
        {
            if (cnt.count(s[i] - k)) res += cnt[s[i] - k];
            cnt[s[i]] ++;
        }
        return res;
    }
};
```