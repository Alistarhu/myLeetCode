# 94. Binary Tree Inorder Traversal - Medium

## Description
Given a binary tree, return the inorder traversal of its nodes' values.

## Example
```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```

## Analysis
题目要求输出一个二叉树的中序遍历结果，中序遍历：由左到中到右。二叉树属于递归的结构，二叉树的题目很适合采用递归方法进行求解，这里采用递归方法进行求解(二叉树的题目也可以采用循环的非递归方法)。

## Solution
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        backtrack(root, res);
        return res;
    }
    void backtrack(TreeNode* root, vector<int>& res)
    {
        if(root==NULL)
            return;
        backtrack(root->left, res);
        res.push_back(root->val);
        backtrack(root->right, res);
    }
};
```
