
# 105. Construct Binary Tree from Preorder and Inorder Traversal - 从前序与中序遍历序列构造二叉树

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given two integer arrays <code>preorder</code> and <code>inorder</code> where <code>preorder</code> is the preorder traversal of a binary tree and <code>inorder</code> is the inorder traversal of the same tree, construct and return <em>the binary tree</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" style="width: 277px; height: 302px;" />
<pre>
<strong>Input:</strong> preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
<strong>Output:</strong> [3,9,20,null,null,15,7]
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> preorder = [-1], inorder = [-1]
<strong>Output:</strong> [-1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= preorder.length &lt;= 3000</code></li>
	<li><code>inorder.length == preorder.length</code></li>
	<li><code>-3000 &lt;= preorder[i], inorder[i] &lt;= 3000</code></li>
	<li><code>preorder</code> and <code>inorder</code> consist of <strong>unique</strong> values.</li>
	<li>Each value of <code>inorder</code> also appears in <code>preorder</code>.</li>
	<li><code>preorder</code> is <strong>guaranteed</strong> to be the preorder traversal of the tree.</li>
	<li><code>inorder</code> is <strong>guaranteed</strong> to be the inorder traversal of the tree.</li>
</ul>


### ZH-CN:
<p>给定两个整数数组&nbsp;<code>preorder</code> 和 <code>inorder</code>&nbsp;，其中&nbsp;<code>preorder</code> 是二叉树的<strong>先序遍历</strong>， <code>inorder</code>&nbsp;是同一棵树的<strong>中序遍历</strong>，请构造二叉树并返回其根节点。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" style="height: 302px; width: 277px;" />
<pre>
<strong>输入</strong><strong>:</strong> preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
<strong>输出:</strong> [3,9,20,null,null,15,7]
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> preorder = [-1], inorder = [-1]
<strong>输出:</strong> [-1]
</pre>

<p>&nbsp;</p>

<p><strong>提示:</strong></p>

<ul>
	<li><code>1 &lt;= preorder.length &lt;= 3000</code></li>
	<li><code>inorder.length == preorder.length</code></li>
	<li><code>-3000 &lt;= preorder[i], inorder[i] &lt;= 3000</code></li>
	<li><code>preorder</code>&nbsp;和&nbsp;<code>inorder</code>&nbsp;均 <strong>无重复</strong> 元素</li>
	<li><code>inorder</code>&nbsp;均出现在&nbsp;<code>preorder</code></li>
	<li><code>preorder</code>&nbsp;<strong>保证</strong> 为二叉树的前序遍历序列</li>
	<li><code>inorder</code>&nbsp;<strong>保证</strong> 为二叉树的中序遍历序列</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 36 ms | 25.4 MB | 2021/04/06 9:36 |

```cpp

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
/*原理讲解：
1. 先序遍历数组第一个元素值就是根节点的值
2. 根节点将中序遍历数组分为两部分，左边是左子树的节点值，右边是右子树的节点值
3. 先序和中序对应同一个二叉树，所以确定先序的子树节点区间时，可以借助中序数组来计算，
   二叉树左子树的节点个数即为中序数组中根节点左边的节点数
*/
class Solution {
public:
    /* 主函数 
    输入: 二叉树的前序遍历数组引用, 二叉树的中序遍历数组引用
    输出: 构造出的二叉树的根节点
    操作: 传入参数，调用build()递归函数
    */
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return build(preorder,0,preorder.size()-1,inorder,0,inorder.size()-1);
    }

    /* 递归的构造函数
    输入：二叉树的前序遍历数组引用, 前序遍历数组当前区间的起始下标，前序遍历数组当前区间的末尾下标，
          二叉树的中序遍历数组引用，中序遍历数组当前区间的起始下标，中序遍历数组当前区间的末尾下标
    输出：构造出的二叉树的根节点
    操作：
    - a. 读取当前根节点的值(也就是先序遍历数组当前区间第一个元素的值)
    - b. 找出当前根节点在中序遍历数组中的索引(以确定构造左右子树对应的中序遍历数组下标区间)
    - c. 确定当前根节点左子树的个数(以确定构造左右子树对应的先序遍历数组下标区间)
    - d. 构造出当前根节点
    - e. 递归调用构造当前根节点左右子树
    */
    TreeNode* build(vector<int>& preorder, int preStart, int preEnd,
                    vector<int>& inorder, int inStart, int inEnd){
        /*0.变量定义及初始化*/
        int rootVal = 0; //当前根节点值
        int index = 0; //当前根节点在中序遍历数组中的下标
        int leftSize = 0; //当前根节点左子树的节点个数

        /*1.出口条件*/
        //*1.1 最深层调用返回出口
        if(preStart > preEnd) return nullptr;

        /*2.本层处理*/
        //a. 读取当前根节点值
        rootVal = preorder[preStart];

        //b. 找到当前根节点在中序遍历数组中的索引
        for(int i=inStart;i<=inEnd;i++){
            if(inorder[i]==rootVal)
                index = i;
        }

        //c. 确定当前根节点左子树的节点个数
        leftSize = index - inStart;

        //d. 构建当前根节点    
        TreeNode* root = new TreeNode(rootVal);
        
        /*3.递归调用*/
        //e. 递归构建当前根节点左右子树
        root->left = build(preorder,preStart+1,preStart+leftSize,inorder,inStart,index-1); 
        root->right = build(preorder,preStart+leftSize+1,preEnd,inorder,index+1,inEnd);
        
        //*1.2 处理结果返回出口
        return root;
    }
};

```
## My Notes - 我的笔记


No notes

