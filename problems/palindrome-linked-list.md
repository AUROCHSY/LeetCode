
# 234. Palindrome Linked List - 回文链表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>head</code> of a singly linked list, return <code>true</code> if it is a palindrome.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg" style="width: 422px; height: 62px;" />
<pre>
<strong>Input:</strong> head = [1,2,2,1]
<strong>Output:</strong> true
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg" style="width: 182px; height: 62px;" />
<pre>
<strong>Input:</strong> head = [1,2]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is in the range <code>[1, 10<sup>5</sup>]</code>.</li>
	<li><code>0 &lt;= Node.val &lt;= 9</code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you do it in <code>O(n)</code> time and <code>O(1)</code> space?

### ZH-CN:
<p>给你一个单链表的头节点 <code>head</code> ，请你判断该链表是否为回文链表。如果是，返回 <code>true</code> ；否则，返回 <code>false</code> 。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg" style="width: 422px; height: 62px;" />
<pre>
<strong>输入：</strong>head = [1,2,2,1]
<strong>输出：</strong>true
</pre>

<p><strong>示例 2：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg" style="width: 182px; height: 62px;" />
<pre>
<strong>输入：</strong>head = [1,2]
<strong>输出：</strong>false
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li>链表中节点数目在范围<code>[1, 10<sup>5</sup>]</code> 内</li>
	<li><code>0 &lt;= Node.val &lt;= 9</code></li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>你能否用&nbsp;<code>O(n)</code> 时间复杂度和 <code>O(1)</code> 空间复杂度解决此题？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/palindrome-linked-list/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/palindrome-linked-list/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 296 ms | 118.2 MB | 2021/04/04 20:57 |

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
 
/*递归解法*/
/*
思路：
1. 递归函数实现从后往前比较
2. 为了实现前半部分顺序遍历，后半部分逆序遍历，需要在递归函数外定义一个全局函数，在主函数内初始化，在递归函数内更新(实际上进行的是frontPointer从前到后，递归从后到前对整个链表比较)
*/
class Solution {  
    ListNode *frontPointer;//定义一个全局变量作为从头到尾的扫描指针
public:
    /*递归函数：将传入的链表从尾到头扫描并于frontPointer指向的节点比较*/
    bool recursivelyCheck(ListNode* currentNode){
        /*变量定义及初始化*/
        bool res=true;//检查结果，初始化为true，若不匹配则置为false

        /*递归出口*/
        if(currentNode==nullptr)
            return true;

        /*递归调用*/ 
        if(!recursivelyCheck(currentNode->next))//要先判断深层的匹配情况，所以递归调用写在前
            res=false;;

        /*当前层处理*/
        //* 处理
        if(currentNode->val!=frontPointer->val)
            res=false;
        frontPointer=frontPointer->next;//别忘了将frontPointer移向下一节点
        //* 处理结果返回出口
        return res;
    }
    /*主函数*/
    bool isPalindrome(ListNode* head) {
        frontPointer=head;
        return recursivelyCheck(head);
    }
};

```
## My Notes - 我的笔记


No notes

