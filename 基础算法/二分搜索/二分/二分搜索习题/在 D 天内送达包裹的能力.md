# 在 D 天内送达包裹的能力
[LeetCode 1011. 在 D 天内送达包裹的能力](https://leetcode.cn/problems/capacity-to-ship-packages-within-d-days/)

# 解题思路
- 符合条件的运载重量一定是单调的，即如果 $m$ 满足条件，则大于 $m$ 的所有重量都是满足条件的，我们可以通过二分查找满足条件的最小的 $m$
- 假设我们二分到了一个重量 $m$ ，可以通过一次遍历来判断需要多少天来完成装载，如果某个物品的重量大于 $m$ ，或装载的天数大于 $D$，则继续向上二分 $m$

### Code
```cpp
class Solution {
public:
    bool vaild(vector<int>& weights, int days, int volume)
    {
        int date = 1;
        int cur = 0;
        for (auto i : weights)
        {
            if (cur + i <= volume) cur += i;
            else 
            {
                cur = i, date ++;
                if (date > days) return false;
            }
        }
        return date <= days;
    }

    int shipWithinDays(vector<int>& weights, int days) {
        int l = 0, r = 0;
        for (auto i : weights) r += i, l = max(l, i);
        while (l < r)
        {
            int mid = (l + r) >> 1;
            if (vaild(weights, days, mid)) r = mid;
            else l = mid + 1;
        }
        return l;
    }
};
```