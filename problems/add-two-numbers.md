
# 2. Add Two Numbers - 两数相加

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Recursion-递归-blue.svg">   <img src="https://img.shields.io/badge/Linked List-链表-blue.svg">   <img src="https://img.shields.io/badge/Math-数学-blue.svg">  


## Description - 题目描述

### EN:
<p>You are given two <strong>non-empty</strong> linked lists representing two non-negative integers. The digits are stored in <strong>reverse order</strong>, and each of their nodes contains a single digit. Add the two numbers and return the sum&nbsp;as a linked list.</p>

<p>You may assume the two numbers do not contain any leading zero, except the number 0 itself.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg" style="width: 483px; height: 342px;" />
<pre>
<strong>Input:</strong> l1 = [2,4,3], l2 = [5,6,4]
<strong>Output:</strong> [7,0,8]
<strong>Explanation:</strong> 342 + 465 = 807.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> l1 = [0], l2 = [0]
<strong>Output:</strong> [0]
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
<strong>Output:</strong> [8,9,9,9,0,0,0,1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in each linked list is in the range <code>[1, 100]</code>.</li>
	<li><code>0 &lt;= Node.val &lt;= 9</code></li>
	<li>It is guaranteed that the list represents a number that does not have leading zeros.</li>
</ul>


### ZH-CN:
<p>给你两个 <strong>非空</strong> 的链表，表示两个非负的整数。它们每位数字都是按照 <strong>逆序</strong> 的方式存储的，并且每个节点只能存储 <strong>一位</strong> 数字。</p>

<p>请你将两个数相加，并以相同形式返回一个表示和的链表。</p>

<p>你可以假设除了数字 0 之外，这两个数都不会以 0 开头。</p>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/01/02/addtwonumber1.jpg" style="width: 483px; height: 342px;" />
<pre>
<strong>输入：</strong>l1 = [2,4,3], l2 = [5,6,4]
<strong>输出：</strong>[7,0,8]
<strong>解释：</strong>342 + 465 = 807.
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>l1 = [0], l2 = [0]
<strong>输出：</strong>[0]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
<strong>输出：</strong>[8,9,9,9,0,0,0,1]
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li>每个链表中的节点数在范围 <code>[1, 100]</code> 内</li>
	<li><code>0 <= Node.val <= 9</code></li>
	<li>题目数据保证列表表示的数字不含前导零</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/add-two-numbers/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/add-two-numbers/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 32 ms | 69.5 MB | 2021/03/26 15:45 |

```cpp

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}//预定义的构造函数,调用该函数生成一个结点，值为0,next指针为nullptr(也就是NULL)
 *     ListNode(int x) : val(x), next(nullptr) {} //传入结点值的构造函数
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}//传入结点值和下一个结点指针的构造函数
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *head=NULL,*tail=NULL;//结果链表的头尾指针
        int n1=0,n2=0,sum=0;//存储参与加法运算的两个数及它们的和
        int carry=0;//进位
        while(l1 || l2){
           n1= l1 ? l1->val : 0; ////如果l1为空,则判定为false,将0赋值给n1
           n2= l2 ? l2->val : 0;
           sum=n1+n2+carry;
           if(!head){//结构链表第一个结点的初始化，将头指针和尾指针指向它
               head=tail=new ListNode(sum % 10);//将求和结果进位后剩余的数赋值给结果链表结点
           }
           else{
               tail->next=new ListNode(sum % 10);
               tail=tail->next;    
           }
           carry=sum / 10; //计算进位。如果sum>=10，进位为1，否则为0
           if(l1){
               l1=l1->next;
           }
           if(l2){
               l2=l2->next;
           }    
        }
        if(carry>0){////遍历完l1和l2后，若最后一位还有进位，别忘了加上
            tail->next=new ListNode(carry);
            tail=tail->next;//这句有没有都行，若无这句则tail指向倒数第二个结点
        }
        return head;
    }    
};

```
## My Notes - 我的笔记


No notes

