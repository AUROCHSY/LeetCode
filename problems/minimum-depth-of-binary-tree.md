
# 111. Minimum Depth of Binary Tree - 二叉树的最小深度

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth-First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth-First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a binary tree, find its minimum depth.</p>

<p>The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.</p>

<p><strong>Note:</strong>&nbsp;A leaf is a node with no children.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg" style="width: 432px; height: 302px;" />
<pre>
<strong>Input:</strong> root = [3,9,20,null,null,15,7]
<strong>Output:</strong> 2
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = [2,null,3,null,4,null,5,null,6]
<strong>Output:</strong> 5
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 10<sup>5</sup>]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
</ul>


### ZH-CN:
<p>给定一个二叉树，找出其最小深度。</p>

<p>最小深度是从根节点到最近叶子节点的最短路径上的节点数量。</p>

<p><strong>说明：</strong>叶子节点是指没有子节点的节点。</p>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg" style="width: 432px; height: 302px;" />
<pre>
<strong>输入：</strong>root = [3,9,20,null,null,15,7]
<strong>输出：</strong>2
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>root = [2,null,3,null,4,null,5,null,6]
<strong>输出：</strong>5
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li>树中节点数的范围在 <code>[0, 10<sup>5</sup>]</code> 内</li>
	<li><code>-1000 <= Node.val <= 1000</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 276 ms | 141.3 MB | 2021/03/30 20:10 |

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

/*解法二：广度优先搜索(层序遍历)*/
/*
思路：
借助队列进行层序遍历
0. 根结点为空特例处理
1. 遇到第一个叶子节点，则该叶子节点的深度就是题目要求的最小深度
2. 否则接着进行层序遍历
*/
class Solution {
public:
    int minDepth(TreeNode *root) {
        
        /*变量定义及初始化*/
        //queue为队列，其结点为元素对,两个参数分别为结点 first 值和 second 值的类型
        //其中first值存储树节点指针，second值存储树的深度
        queue< pair<TreeNode*,int> > q;
        TreeNode *node = nullptr; //记录当前队头节点指针
        int depth = 0; //记录当前队头节点深度

        /*算法主体*/
        //处理特例
        if(root==nullptr)
            return 0;

        //一般情况
        q.emplace(root,1);//根节点入队
        while(!q.empty()){//队列非空
            
            //读取队头节点
            node = q.front().first; //读取队头节点指针
            depth = q.front().second; //读取队头节点深度

            //队头节点出队
            q.pop();

            //判断当前节点是否为叶子节点,如果是则返回其深度。题目要求的最小深度即为层序遍历的第一个叶子结点的深度
            if(node->left==nullptr && node->right==nullptr)
                return depth;

            //如果不是叶子节点，则接着进行层序遍历

            if(node->left!=nullptr) //左子树非空，将左子节点入队
                q.emplace(node->left,depth+1);

            if(node->right!=nullptr)//右子树非空，将左子节点入队
                q.emplace(node->right,depth+1);

        }

        /*返回结果*/
        return 0; //其实不会执行到这句，前面已经囊括所有情况了，只是编译器要求在这加个return避免有没处理到的情况
 }      
};

```
## My Notes - 我的笔记


No notes

