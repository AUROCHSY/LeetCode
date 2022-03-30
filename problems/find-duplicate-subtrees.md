
# 652. Find Duplicate Subtrees - 寻找重复的子树

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth-First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Hash Table-哈希表-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>root</code>&nbsp;of a binary tree, return all <strong>duplicate subtrees</strong>.</p>

<p>For each kind of duplicate subtrees, you only need to return the root node of any <b>one</b> of them.</p>

<p>Two trees are <strong>duplicate</strong> if they have the <strong>same structure</strong> with the <strong>same node values</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/08/16/e1.jpg" style="width: 450px; height: 354px;" />
<pre>
<strong>Input:</strong> root = [1,2,3,4,null,2,4,null,null,4]
<strong>Output:</strong> [[2,4],[4]]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/08/16/e2.jpg" style="width: 321px; height: 201px;" />
<pre>
<strong>Input:</strong> root = [2,1,1]
<strong>Output:</strong> [[1]]
</pre>

<p><strong>Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/08/16/e33.jpg" style="width: 450px; height: 303px;" />
<pre>
<strong>Input:</strong> root = [2,2,2,3,null,3,null]
<strong>Output:</strong> [[2,3],[3]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of the nodes in the tree will be in the range <code>[1, 10^4]</code></li>
	<li><code>-200 &lt;= Node.val &lt;= 200</code></li>
</ul>


### ZH-CN:
<p>给定一棵二叉树 <code>root</code>，返回所有<strong>重复的子树</strong>。</p>

<p>对于同一类的重复子树，你只需要返回其中任意<strong>一棵</strong>的根结点即可。</p>

<p>如果两棵树具有<strong>相同的结构</strong>和<strong>相同的结点值</strong>，则它们是<strong>重复</strong>的。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2020/08/16/e1.jpg" style="height: 236px; width: 300px;" /></p>

<pre>
<strong>输入：</strong>root = [1,2,3,4,null,2,4,null,null,4]
<strong>输出：</strong>[[2,4],[4]]</pre>

<p><strong>示例 2：</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2020/08/16/e2.jpg" style="height: 125px; width: 200px;" /></p>

<pre>
<strong>输入：</strong>root = [2,1,1]
<strong>输出：</strong>[[1]]</pre>

<p><strong>示例 3：</strong></p>

<p><strong><img alt="" src="https://assets.leetcode.com/uploads/2020/08/16/e33.jpg" style="height: 202px; width: 300px;" /></strong></p>

<pre>
<strong>输入：</strong>root = [2,2,2,3,null,3,null]
<strong>输出：</strong>[[2,3],[3]]</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li>树中的结点数在<code>[1,10^4]</code>范围内。</li>
	<li><code>-200 &lt;= Node.val &lt;= 200</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/find-duplicate-subtrees/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/find-duplicate-subtrees/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 56 ms | 63.5 MB | 2021/04/06 18:37 |

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
class Solution {
private:
    /*全局变量：下面函数对它们的修改都会生效*/
    unordered_map<string,int> allTrees;
    vector<TreeNode*> res;

public:
    /* 主函数
    输入: 待处理二叉树的根节点指针
    输出: 一个数组, 元素为重复出现的子树的根节点
    操作: 
    - a.调用traverse()函数, 该函数会对全局变量 memo 和 res 进行修改，它返回给主函数的序列化子树并不需要接收。
    - b.返回已被traverse() 修改的全局变量 res
     */
    vector<TreeNode*> findDuplicateSubtrees(TreeNode* root) {
        traverse(root);
        return res;
    }

    /* 辅助函数
    输入: 当前待处理二叉树的根结点指针
    输出: 
     - return 直接输出：当前待处理二叉树的序列化字符串
     - 通过修改全局变量隐式输出：memo记录所有子树及其出现次数, res记录重复子树的根节点
    操作: 
    - a. 递归调用对当前根节点的左子树和右子树进行处理
    - b. 序列化当前根节点所对应子树为字符串(以后序遍历的顺序)，对空节点用 "#" 标记
    - c. 记录子树的出现次数
    - d. 在子树重复(第二次)出现时将其加入结果数组 res
     */
    string traverse(TreeNode* root) {
        /*0.变量定义及初始化*/
        string leftChild;
        string rightChild;
        string subTree;

        /*1.递归出口*/
        //*1.1 最深层调用返回出口
        if(root==nullptr) return "#";

        /*2.递归调用*/
        //a. 递归调用处理当前根节点的左右子树
        leftChild = traverse(root->left);
        rightChild = traverse(root->right);


        /*3.本层处理*/
        //b. 序列化当前子树为字符串
        subTree = leftChild + "," + rightChild + "," + to_string(root->val);
        
        //c. 将当前子树添加到全部子树集里(更新个数)
        allTrees[subTree]++;

        //d. 若是重复(第二次)出现，则将当前子树的根节点添加到结果数组里
        if(allTrees[subTree]==2)
            res.push_back(root);

        //*1.2 处理结果返回出口
        return subTree;

    }
};

```
## My Notes - 我的笔记


No notes

