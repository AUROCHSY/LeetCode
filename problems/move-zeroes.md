
# 283. Move Zeroes - 移动零

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array <code>nums</code>, move all <code>0</code>&#39;s to the end of it while maintaining the relative order of the non-zero elements.</p>

<p><strong>Note</strong> that you must do this in-place without making a copy of the array.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [0,1,0,3,12]
<strong>Output:</strong> [1,3,12,0,0]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [0]
<strong>Output:</strong> [0]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-2<sup>31</sup> &lt;= nums[i] &lt;= 2<sup>31</sup> - 1</code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you minimize the total number of operations done?

### ZH-CN:
<p>给定一个数组 <code>nums</code>，编写一个函数将所有 <code>0</code> 移动到数组的末尾，同时保持非零元素的相对顺序。</p>

<p><strong>请注意</strong>&nbsp;，必须在不复制数组的情况下原地对数组进行操作。</p>

<p>&nbsp;</p>

<p><strong>示例 1:</strong></p>

<pre>
<strong>输入:</strong> nums = <code>[0,1,0,3,12]</code>
<strong>输出:</strong> <code>[1,3,12,0,0]</code>
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> nums = <code>[0]</code>
<strong>输出:</strong> <code>[0]</code></pre>

<p>&nbsp;</p>

<p><strong>提示</strong>:</p>
<meta charset="UTF-8" />

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-2<sup>31</sup>&nbsp;&lt;= nums[i] &lt;= 2<sup>31</sup>&nbsp;- 1</code></li>
</ul>

<p>&nbsp;</p>

<p><b>进阶：</b>你能尽量减少完成的操作次数吗？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/move-zeroes/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/move-zeroes/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 4 ms | 8.8 MB | 2021/03/29 21:37 |

```cpp

/*
注意：不能更换元素的相对次序，所以不能用头尾相向扫描交换
思路：
- 两个指针同向前进
- 遇到0元素时i指针停留，此时nums[i]=0,j指针继续前进
- j指针遇到非0元素时，将其赋值给nums[i],并将0交换给nums[j];i++;j++;
循环直至j到达数组末尾
*/
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        /*变量定义及初始化*/
        int i=0;//始终指向第一个0元素
        int j=0;//遍历指针
        
        /*函数主体*/        
        //处理特例:输入数组只有1个0元素时
        if(nums.size()==1)
            return;    
        //一般情况
        while(j<nums.size()){
            while(j<nums.size() && nums[i]!=0){//退出while循环时i,j指向第一个0元素
                i++;
                j++;
            }

            while(j<nums.size() && nums[j]==0)//退出while循环时j指向第一个非0元素
                j++;
            if(j<nums.size()){
                nums[i]=nums[j];
                nums[j]=0;//0元素还是要保留的，只不过要挪到后面
                i++;
                j++;
            }
        }

        /*返回结果:无(直接在原数组上操作)*/
    }
};

```
## My Notes - 我的笔记


No notes

