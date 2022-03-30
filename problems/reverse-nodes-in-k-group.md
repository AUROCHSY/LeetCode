
# 25. Reverse Nodes in k-Group - K 个一组翻转链表

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>head</code> of a linked list, reverse the nodes of the list <code>k</code> at a time, and return <em>the modified list</em>.</p>

<p><code>k</code> is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of <code>k</code> then left-out nodes, in the end, should remain as it is.</p>

<p>You may not alter the values in the list&#39;s nodes, only nodes themselves may be changed.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg" style="width: 542px; height: 222px;" />
<pre>
<strong>Input:</strong> head = [1,2,3,4,5], k = 2
<strong>Output:</strong> [2,1,4,3,5]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg" style="width: 542px; height: 222px;" />
<pre>
<strong>Input:</strong> head = [1,2,3,4,5], k = 3
<strong>Output:</strong> [3,2,1,4,5]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is <code>n</code>.</li>
	<li><code>1 &lt;= k &lt;= n &lt;= 5000</code></li>
	<li><code>0 &lt;= Node.val &lt;= 1000</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow-up:</strong> Can you solve the problem in <code>O(1)</code> extra memory space?</p>


### ZH-CN:
<p>给你一个链表，每 <em>k </em>个节点一组进行翻转，请你返回翻转后的链表。</p>

<p><em>k </em>是一个正整数，它的值小于或等于链表的长度。</p>

<p>如果节点总数不是 <em>k </em>的整数倍，那么请将最后剩余的节点保持原有顺序。</p>

<p><strong>进阶：</strong></p>

<ul>
	<li>你可以设计一个只使用常数额外空间的算法来解决此问题吗？</li>
	<li><strong>你不能只是单纯的改变节点内部的值</strong>，而是需要实际进行节点交换。</li>
</ul>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg" style="width: 542px; height: 222px;" />
<pre>
<strong>输入：</strong>head = [1,2,3,4,5], k = 2
<strong>输出：</strong>[2,1,4,3,5]
</pre>

<p><strong>示例 2：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg" style="width: 542px; height: 222px;" />
<pre>
<strong>输入：</strong>head = [1,2,3,4,5], k = 3
<strong>输出：</strong>[3,2,1,4,5]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>head = [1,2,3,4,5], k = 1
<strong>输出：</strong>[1,2,3,4,5]
</pre>

<p><strong>示例 4：</strong></p>

<pre>
<strong>输入：</strong>head = [1], k = 1
<strong>输出：</strong>[1]
</pre>

<ul>
</ul>

<p><strong>提示：</strong></p>

<ul>
	<li>列表中节点的数量在范围 <code>sz</code> 内</li>
	<li><code>1 <= sz <= 5000</code></li>
	<li><code>0 <= Node.val <= 1000</code></li>
	<li><code>1 <= k <= sz</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/reverse-nodes-in-k-group/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 32 ms | 11.2 MB | 2021/04/04 15:16 |

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
    /**反转函数：反转区间 [leftNode, rightNode) 的元素，注意是左闭右开 */
    ListNode* reverse(ListNode* leftNode, ListNode* rightNode) {
        
        /*变量声明及初始化*/
        ListNode *prev=nullptr;
        ListNode *curr = leftNode; 
        ListNode *next = leftNode;

        // while 终止的条件改一下就行了
        while (curr != rightNode) {
            next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        
        /*返回结果：返回反转后的头结点*/
        return prev;
    }

    /*主函数(递归)：递归调用不断反转前k个元素*/
    ListNode* reverseKGroup(ListNode* head, int k) {
        
        /*0. 变量定义及初始化*/
        ListNode *leftNode, *rightNode;
        leftNode = rightNode = head;
        int i=0;

        /*1. 出口条件*/
        //*1.1 第一层特例处理出口
        if (head == nullptr) 
            return nullptr;


        /*2. 当前层操作主体*/
        //*2.1-1 操作：将rightNode移到正确的位置
        while(i<k && rightNode!=nullptr){ //注意若[leftNode,rightNode)需含k个元素，区间是左开右闭的
            rightNode=rightNode->next;
            i++;
        }

        //*1.2  第一层特例处理出口 & 最深层递归返回出口
        if(i!=k && rightNode==nullptr) //最后一批不足k个，无需反转直接返回
            return head;
        
        //*2.1-2 操作：反转[leftNode,rightNode)之间的 k 个元素
        ListNode* newHead = reverse(leftNode, rightNode); 

        /*3. 递归调用：每k个一批反转后续链表*/
        leftNode->next = reverseKGroup(rightNode, k);

        //2.2 操作后的返回
        return newHead;
    }

};


```
## My Notes - 我的笔记


No notes

