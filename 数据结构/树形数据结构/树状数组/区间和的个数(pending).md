# 区间和的个数
[LeetCode 327. 区间和的个数](https://leetcode.cn/problems/count-of-range-sum/)

# 解题思路1
$O(nlog⁡n)$
- 我们采取分治的思想。首先求出前缀和数组（包括开头的 $0$）$sum$，在这个数组上采用分治算法：每次将数组平均分为两部分，递归处理左右两部分内部的答案，然后将左右两部分内部从小到大排序，最后归并跨越左右两部分的答案。
- 接下来讨论如何求跨越两部分的答案：假设左右两部分已经从小到大排好序，我们设 $i$ 为右部分的某个位置，对于每个 $i$，都有一个在左部分连续的区间 $[j, k]$， 对应着合法答案的区间，即 `sum[i] - sum[j], sum[i] - sum[j + 1], ..., sum[i] - sum[k]` 都是在 $[lower, upper]$ 中。随着 $i$ 向右移动，这个区间也会整体向右移动。这给我们提供了滑动窗口的思想，我们用双指针实时维护这个窗口，可以在均摊 $O(1)$ 的时间内找到每个 $i$ 对应的区间。
- 然后利用归并排序的思想将当前区间排序。

### Code
```cpp
class Solution {
public:
    int lower, upper;
    vector<long long> w;
    long long merge_sort(vector<long long>& s, int l, int r)
    {
        if (l >= r) return 0;
        int mid = (l + r) >> 1;
        int res = merge_sort(s, l, mid) + merge_sort(s, mid + 1, r);

        for (int i = l, j = mid + 1, t = j; i <= mid; i ++)
        {
            while (j <= r && s[j] - s[i] < lower) j ++;
            while (t <= r && s[t] - s[i] <= upper) t ++;
            res += t - j;
        }

        w.clear();
        int i = l, j = mid + 1;
        while (i <= mid && j <= r)
            if (s[i] <= s[j]) w.push_back(s[i ++]);
            else w.push_back(s[j ++]);
        while (i <= mid) w.push_back(s[i ++]);
        while (j <= r) w.push_back(s[j ++]);
        for (int i = l, j = 0; j < w.size(); i ++, j ++) s[i] = w[j];
        return res;
    }

    int countRangeSum(vector<int>& nums, int lower, int upper)
    {
        int n = nums.size();
        this->lower = lower;
        this->upper = upper;
        vector<long long> sum(n + 1);
        for (int i = 1; i <= n; i ++) sum[i] = sum[i - 1] + nums[i - 1];
        return merge_sort(sum, 0, n);
    }
};
```

# 解题思路2
树状数组