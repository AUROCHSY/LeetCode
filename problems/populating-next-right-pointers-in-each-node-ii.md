
# 117. Populating Next Right Pointers in Each Node II - 填充每个节点的下一个右侧节点指针 II

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth-First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth-First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Given a binary tree</p>

<pre>
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
</pre>

<p>Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to <code>NULL</code>.</p>

<p>Initially, all next pointers are set to <code>NULL</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/02/15/117_sample.png" style="width: 500px; height: 171px;" />
<pre>
<strong>Input:</strong> root = [1,2,3,4,5,null,7]
<strong>Output:</strong> [1,#,2,3,#,4,5,7,#]
<strong>Explanation: </strong>Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with &#39;#&#39; signifying the end of each level.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 6000]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow-up:</strong></p>

<ul>
	<li>You may only use constant extra space.</li>
	<li>The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.</li>
</ul>


### ZH-CN:
<p>给定一个二叉树</p>

<pre>
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}</pre>

<p>填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 <code>NULL</code>。</p>

<p>初始状态下，所有 next 指针都被设置为 <code>NULL</code>。</p>

<p> </p>

<p><strong>进阶：</strong></p>

<ul>
	<li>你只能使用常量级额外空间。</li>
	<li>使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。</li>
</ul>

<p> </p>

<p><strong>示例：</strong></p>

<p><img alt="" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/15/117_sample.png" style="height: 218px; width: 640px;" /></p>

<pre>
<strong>输入</strong>：root = [1,2,3,4,5,null,7]
<strong>输出：</strong>[1,#,2,3,#,4,5,7,#]
<strong>解释：</strong>给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。序列化输出按层序遍历顺序（由 next 指针连接），'#' 表示每层的末尾。</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li>树中的节点数小于 <code>6000</code></li>
	<li><code>-100 <= node.val <= 100</code></li>
</ul>

<p> </p>

<ul>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 16 ms | 17 MB | 2021/04/02 11:14 |

```cpp

/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

/*解法二：使用已建立的next指针(类似于层序遍历)*/
class Solution {
public:
    /*建立上一个子节点与当前子节点的next连接；更新下一层起始节点指针*/
    void handle(Node* &lastChild,Node* &pchild,Node* &nextStart){ //传入引用型参数，以使得此处的修改对原链表生效
        //* 建立上一个子节点与当前子节点的next连接
        if(lastChild!=nullptr)
            lastChild->next=pchild;
        lastChild=pchild;

        //* 更新下一层起始节点指针
        if(nextStart==nullptr) //如果nextStart为空，则会一直将其更新为pchild，直至其为子节点层的第一个非空节点
            nextStart=pchild;
    }

    /*主函数*/
    Node* connect(Node* root) {
        /*变量定义及初始化*/
        Node* start=nullptr; //当前层最左侧非空节点
        Node* nextStart=nullptr; //下一层最左侧非空节点(因为不是满二叉树，所以nextStart不一定等于start->left)
        Node* p=nullptr; //当前层扫描指针
        Node* lastChild=nullptr; //上一个进行连接的子节点(遍历p所在层时，进行的操作是连接p的下一层(子节点))
        
        /*算法主体*/
        //* 处理特例
        if(!root)//空树
            return root;

        //* 一般情况
        start=root;//从根节点开始(第一层的最左节点)
        while(start){ //遍历层数
            lastChild=nullptr; //每次进入新层都将lastchild和nextStart置为null，以便handle()函数对其进行操作
            nextStart=nullptr;
            for(p=start;p!=nullptr;p=p->next){ //遍历当前层全部节点
                if(p->left!=nullptr)
                    handle(lastChild,p->left,nextStart);//连接子节点；更新下一层起始节点nextStart
                if(p->right!=nullptr)
                    handle(lastChild,p->right,nextStart);
            }
            start=nextStart;//进入下一层
        }

        /*返回结果*/
        return root;
    }
};

```
## My Notes - 我的笔记


No notes

