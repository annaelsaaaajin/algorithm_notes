# N叉树的前序遍历
[LeetCode 589. N叉树的前序遍历](https://leetcode.cn/problems/n-ary-tree-preorder-traversal/submissions/)

# Code
```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
public:
    vector<int> ans;
    void dfs(Node* root)
    {
        if (root == nullptr) return;
        ans.push_back(root->val);
        for (auto i : root->children) dfs(i);
    }
    vector<int> preorder(Node* root) {
        dfs(root);
        return ans;
    }
};
```