
# 110. Balanced Binary Tree - 平衡二叉树

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth-First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a binary tree, determine if it is height-balanced.</p>

<p>For this problem, a height-balanced binary tree is defined as:</p>

<blockquote>
<p>a binary tree in which the left and right subtrees of <em>every</em> node differ in height by no more than 1.</p>
</blockquote>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg" style="width: 342px; height: 221px;" />
<pre>
<strong>Input:</strong> root = [3,9,20,null,null,15,7]
<strong>Output:</strong> true
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg" style="width: 452px; height: 301px;" />
<pre>
<strong>Input:</strong> root = [1,2,2,3,3,null,null,4,4]
<strong>Output:</strong> false
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> root = []
<strong>Output:</strong> true
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 5000]</code>.</li>
	<li><code>-10<sup>4</sup> &lt;= Node.val &lt;= 10<sup>4</sup></code></li>
</ul>


### ZH-CN:
<p>给定一个二叉树，判断它是否是高度平衡的二叉树。</p>

<p>本题中，一棵高度平衡二叉树定义为：</p>

<blockquote>
<p>一个二叉树<em>每个节点 </em>的左右两个子树的高度差的绝对值不超过 1 。</p>
</blockquote>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg" style="width: 342px; height: 221px;" />
<pre>
<strong>输入：</strong>root = [3,9,20,null,null,15,7]
<strong>输出：</strong>true
</pre>

<p><strong>示例 2：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg" style="width: 452px; height: 301px;" />
<pre>
<strong>输入：</strong>root = [1,2,2,3,3,null,null,4,4]
<strong>输出：</strong>false
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>root = []
<strong>输出：</strong>true
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li>树中的节点数在范围 <code>[0, 5000]</code> 内</li>
	<li><code>-10<sup>4</sup> <= Node.val <= 10<sup>4</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/balanced-binary-tree/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/balanced-binary-tree/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 16 ms | 20.2 MB | 2021/03/30 15:45 |

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

/*解法一：自顶向下递归*/

class Solution {
public:
    /*求二叉树高度(递归)*/
    int height(TreeNode* root){
        /*出口条件*/
        if(root==NULL)//当前层子树高度为0
            return 0;

        /*递归调用 + 当前层操作主体(+1)*/
        return max(height(root->left),height(root->right))+1;//当前层子树的高度等于其左右子树的高度中的较大者+1

    }

    /*主函数判断是否是平衡二叉树(递归)*/
    bool isBalanced(TreeNode* root) {
        /*出口条件*/
        if(root==NULL)
            return true;

        /*当前层操作主体 + 递归调用*/   
            return abs(height(root->left) - height(root->right))<=1 && //当前以root为根节点的子树是平衡二叉树
                    isBalanced(root->left) && //root的左子树是平衡二叉树
                    isBalanced(root->right); //root的右子树是平衡二叉树；    
    }
};


/*解法二：自底向上递归*/
// class Solution {
// public:
//     /*求二叉树高度同时判断是否平衡(递归)*/
//     //利用递归自底向上求子树高度并判断是否平衡，若不平衡则返回-1，若平衡则返回高度
//     int height(TreeNode *root){
//         /*出口条件*/
//         if(root==NULL)
//             return 0;

//         /*递归调用*/
//         int leftHeight=height(root->left);
//         int rightHeight=height(root->right);

//         /*当前层操作主体*/
//         if(leftHeight==-1 || rightHeight==-1 || abs(leftHeight-rightHeight)>1 )//左子树不平衡 || 右子树不平衡 || 当前root为根的子树不平衡(左右子树高度差>1)
//             return -1;
//         else
//             return max(leftHeight,rightHeight)+1;//返回当前子树高度
//     }

//     /*主函数*/
//     bool isBalanced(TreeNode* root) {
//         return height(root)>=0; //调用递归函数。若返回高度>=0则平衡，若返回-1则不平衡
//     }
// };

```
## My Notes - 我的笔记


No notes

