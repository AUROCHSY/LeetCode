
# 92. Reverse Linked List II - 反转链表 II

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">  


## Description - 题目描述

### EN:
<p>Given the <code>head</code> of a singly linked list and two integers <code>left</code> and <code>right</code> where <code>left &lt;= right</code>, reverse the nodes of the list from position <code>left</code> to position <code>right</code>, and return <em>the reversed list</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg" style="width: 542px; height: 222px;" />
<pre>
<strong>Input:</strong> head = [1,2,3,4,5], left = 2, right = 4
<strong>Output:</strong> [1,4,3,2,5]
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> head = [5], left = 1, right = 1
<strong>Output:</strong> [5]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is <code>n</code>.</li>
	<li><code>1 &lt;= n &lt;= 500</code></li>
	<li><code>-500 &lt;= Node.val &lt;= 500</code></li>
	<li><code>1 &lt;= left &lt;= right &lt;= n</code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you do it in one pass?

### ZH-CN:
给你单链表的头指针 <code>head</code> 和两个整数 <code>left</code> 和 <code>right</code> ，其中 <code>left <= right</code> 。请你反转从位置 <code>left</code> 到位置 <code>right</code> 的链表节点，返回 <strong>反转后的链表</strong> 。
<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg" style="width: 542px; height: 222px;" />
<pre>
<strong>输入：</strong>head = [1,2,3,4,5], left = 2, right = 4
<strong>输出：</strong>[1,4,3,2,5]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>head = [5], left = 1, right = 1
<strong>输出：</strong>[5]
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li>链表中节点数目为 <code>n</code></li>
	<li><code>1 <= n <= 500</code></li>
	<li><code>-500 <= Node.val <= 500</code></li>
	<li><code>1 <= left <= right <= n</code></li>
</ul>

<p> </p>

<p><strong>进阶：</strong> 你可以使用一趟扫描完成反转吗？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/reverse-linked-list-ii/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/reverse-linked-list-ii/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 0 ms | 7.2 MB | 2021/04/03 20:39 |

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
/* 
思路：
1. 将原链表待反转区间的节点摘下
2. 调用用于反转整个链表的函数，对子链表进行反转
3. 将反转后的子链表拼接回去(注意应该放左边的是right，放右边的是left了)

这里的代码实现中，在第一个数据节点head前面添加了虚拟头节点dummyNode，用以统一对原链表第一个数据节点和其余数据节点的操作
*/
class Solution {
private:
    /*反转函数：反转以head为第一个数据节点的整个链表*/
    void reverseLinkedList(ListNode *head){ 
        ListNode *cur = nullptr;//遍历指针
        ListNode *pre = nullptr;//遍历指针的前驱节点指针
		
    	cur=head;
        while (cur != nullptr) {
            ListNode *next = cur->next;
            cur->next = pre;
            pre = cur;
            cur = next;
        }
    }

public:
    /*主函数*/
    ListNode *reverseBetween(ListNode *head, int left, int right) {
        /*变量定义及初始化*/
        ListNode* dummyNode=new ListNode(-1); //创建虚拟头节点，并用dummyNode指针指向它，其节点值为-1
        ListNode* pre; //扫描指针，pre指向当前操作的节点的前驱节点
        ListNode *rear;
        ListNode* leftNode=nullptr,*rightNode=nullptr;

        /*算法主体*/
        //0.将虚拟头节点指针指向数据头节点
        dummyNode->next = head;
        
        //1.找到链表待反转部分的起始节点left的前驱节点
        pre = dummyNode; 
        for (int i = 0; i < left - 1; i++)
            pre = pre->next;

        //2.找到链表待反转部分的结束节点right
        rightNode = pre;
        for (int i = 0; i < right - left + 1; i++) {
            rightNode = rightNode->next;
        }
        //3.摘下待反转部分的子链表，分别用left和right指向子链表的头尾节点
        leftNode=pre->next;
        pre->next = nullptr;
        rear = rightNode->next;
        rightNode->next = nullptr;

        //4. 对摘下的子链表进行反转，可以把left作为头节点传入，调用用于反转整个链表的函数进行反转
        reverseLinkedList(leftNode);

        //5.子链表反转完毕后再将其接回原链表
        pre->next = rightNode; //注意pre要接的是right不是left了
        leftNode->next = rear;
        
        /*返回结果*/
        return dummyNode->next;//返回数据头节点
    }
};

```
## My Notes - 我的笔记


No notes

