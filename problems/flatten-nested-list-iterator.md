
# 341. Flatten Nested List Iterator - 扁平化嵌套列表迭代器

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Stack-栈-blue.svg">   <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth-First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Design-设计-blue.svg">   <img src="https://img.shields.io/badge/Queue-队列-blue.svg">   <img src="https://img.shields.io/badge/Iterator-迭代器-blue.svg">  


## Description - 题目描述

### EN:
<p>You are given a nested list of integers <code>nestedList</code>. Each element is either an integer or a list whose elements may also be integers or other lists. Implement an iterator to flatten it.</p>

<p>Implement the <code>NestedIterator</code> class:</p>

<ul>
	<li><code>NestedIterator(List&lt;NestedInteger&gt; nestedList)</code> Initializes the iterator with the nested list <code>nestedList</code>.</li>
	<li><code>int next()</code> Returns the next integer in the nested list.</li>
	<li><code>boolean hasNext()</code> Returns <code>true</code> if there are still some integers in the nested list and <code>false</code> otherwise.</li>
</ul>

<p>Your code will be tested with the following pseudocode:</p>

<pre>
initialize iterator with nestedList
res = []
while iterator.hasNext()
    append iterator.next() to the end of res
return res
</pre>

<p>If <code>res</code> matches the expected flattened list, then your code will be judged as correct.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nestedList = [[1,1],2,[1,1]]
<strong>Output:</strong> [1,1,2,1,1]
<strong>Explanation:</strong> By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,1,2,1,1].
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nestedList = [1,[4,[6]]]
<strong>Output:</strong> [1,4,6]
<strong>Explanation:</strong> By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,4,6].
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nestedList.length &lt;= 500</code></li>
	<li>The values of the integers in the nested list is in the range <code>[-10<sup>6</sup>, 10<sup>6</sup>]</code>.</li>
</ul>


### ZH-CN:
<p>给你一个嵌套的整数列表 <code>nestedList</code> 。每个元素要么是一个整数，要么是一个列表；该列表的元素也可能是整数或者是其他列表。请你实现一个迭代器将其扁平化，使之能够遍历这个列表中的所有整数。</p>

<p>实现扁平迭代器类 <code>NestedIterator</code> ：</p>

<ul>
	<li><code>NestedIterator(List&lt;NestedInteger&gt; nestedList)</code> 用嵌套列表 <code>nestedList</code> 初始化迭代器。</li>
	<li><code>int next()</code> 返回嵌套列表的下一个整数。</li>
	<li><code>boolean hasNext()</code> 如果仍然存在待迭代的整数，返回 <code>true</code> ；否则，返回 <code>false</code> 。</li>
</ul>

<p>你的代码将会用下述伪代码检测：</p>

<pre>
initialize iterator with nestedList
res = []
while iterator.hasNext()
    append iterator.next() to the end of res
return res</pre>

<p>如果 <code>res</code> 与预期的扁平化列表匹配，那么你的代码将会被判为正确。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nestedList = [[1,1],2,[1,1]]
<strong>输出：</strong>[1,1,2,1,1]
<strong>解释：</strong>通过重复调用&nbsp;<em>next </em>直到&nbsp;<em>hasNex</em>t 返回 false，<em>next&nbsp;</em>返回的元素的顺序应该是: <code>[1,1,2,1,1]</code>。</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nestedList = [1,[4,[6]]]
<strong>输出：</strong>[1,4,6]
<strong>解释：</strong>通过重复调用&nbsp;<em>next&nbsp;</em>直到&nbsp;<em>hasNex</em>t 返回 false，<em>next&nbsp;</em>返回的元素的顺序应该是: <code>[1,4,6]</code>。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= nestedList.length &lt;= 500</code></li>
	<li>嵌套列表中的整数值在范围 <code>[-10<sup>6</sup>, 10<sup>6</sup>]</code> 内</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/flatten-nested-list-iterator/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/flatten-nested-list-iterator/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 8 ms | 13.1 MB | 2021/04/07 19:29 |

```cpp

/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;  
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */

/* 
问题本质：容易发现其实这就是一个n叉树的问题
题意理解：
本题目的意思是要写一个类，这个类包含两个方法, `next()` 和 `hashNext()` ，要求这两个类实现题目要求的功能。然后这个定义了这个类，其实就相当于定义了一个迭代器(使用方法符合迭代器的定义)。
输入：一个 nestedList列表，该列表的元素可能是单个int整数值，也可能是嵌套的nestedList列表
已知：上面给了几个API,在解题时可以直接调用
输出：编写next()函数和hashNext()函数
        - next()：返回nestedList列表中下一个整数值(如果存在)
        - hashNext()：判断nestedList列表中是否还有整数值(包括嵌套nestedList列表里的整数)

解题思路：
- a. dfs(): 就是n叉树的深度优先遍历的思路, 将嵌套列表扁平化(化为一维列表)
- b. NestedIterator(): 给a的函数包装一个主函数，调用dfs(),返回第一个元素的指针
- c. next(): 题目要求调用该函数时返回下一个整数元素节点，可以通过简单的 `++` 移动指针，使用 `*` 取值
- d. hashNext()：题目要求调用该函数时判断列表里是否还有整数元素，可通过简单的 `cur !=vals.end()` 判断
*/
class NestedIterator {
private:

    /*全局变量*/
    vector<int> vals;
    vector<int>::iterator cur; 

    /*a. 辅助函数：本质就是n叉树的DFS函数, 实现的功能为将多层嵌套列表转化为一维列表*/
    void dfs(const vector<NestedInteger> &nestedList) {
        for(auto &nest : nestedList){
            if(nest.isInteger())
                vals.push_back(nest.getInteger());
            else
                dfs(nest.getList());
        }
    }
public:

    /*b. 主函数：调用dfs()将嵌套列表扁平化, 将 迭代器cur 指向扁平化后的数组的第一个元素*/
    NestedIterator(vector<NestedInteger> &nestedList) {
        dfs(nestedList);
        cur=vals.begin();
    }

    /*题目要求的取下一个整数值的元素*/
    int next() {
        return *cur++;
    }

    /*c. 题目要求的判断列表中是否还有整数值的元素*/
    bool hasNext() {
        return cur != vals.end();
    }
};

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i(nestedList);
 * while (i.hasNext()) cout << i.next();
 */

```
## My Notes - 我的笔记


No notes

