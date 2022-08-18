# 合并K个排序链表
[LeetCode 23. 合并K个排序链表](https://leetcode.cn/problems/merge-k-sorted-lists/submissions/)

# 解题思路1
多路归并分治成二路归并

### Code
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if (lists.empty()) return nullptr;
        return merge(lists, 0, lists.size() - 1);
    }

    ListNode* merge(vector<ListNode*>& lists, int l, int r)
    {
        if (l == r) return lists[l];
        int mid = (l + r) / 2;
        ListNode* l_lists = merge(lists, l, mid);
        ListNode* r_lists = merge(lists, mid + 1, r);
        auto res = mergeTwoLists(l_lists, r_lists);
        return res;
    }

    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode* head;
        if (list1 == nullptr) return list2;
        if (list2 == nullptr) return list1;
        if (list1->val <= list2->val) 
        {
            head = new ListNode(list1->val);
            list1 = list1->next;
        }
        else 
        {
            head = new ListNode(list2->val);
            list2 = list2->next;
        }

        auto cur = head;
        while (list1 != nullptr && list2 != nullptr)
        {
            if (list1->val <= list2->val) 
            {
                auto nextNode = new ListNode(list1->val);
                list1 = list1->next;
                cur->next = nextNode;
                cur = cur->next;
            } 
            else
            {
                auto nextNode = new ListNode(list2->val);
                list2 = list2->next;
                cur->next = nextNode;
                cur = cur->next;
            }
        }

        while (list1 != nullptr)
        {
            auto nextNode = new ListNode(list1->val);
            list1 = list1->next;
            cur->next = nextNode;
            cur = cur->next;
        }

        while (list2 != nullptr)
        {
            auto nextNode = new ListNode(list2->val);
            list2 = list2->next;
            cur->next = nextNode;
            cur = cur->next;
        }
        return head;
    }
};
```

# 解题思路2
直接多路归并，用堆来维护最小值

### Code
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    struct Cmp
    {
        bool operator() (ListNode* a, ListNode* b)
        {
            return a->val > b->val;
        }
    };
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*, vector<ListNode*>, Cmp> heap;
        auto dummy = new ListNode(-1), tail = dummy;
        for (auto l : lists) if (l) heap.push(l);

        while (heap.size())
        {
            auto t = heap.top();
            heap.pop();

            tail = tail->next = t;
            if (t->next) heap.push(t->next);
        }
        return dummy->next;
    }
};
```