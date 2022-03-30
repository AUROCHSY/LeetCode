
# 33. Search in Rotated Sorted Array - 搜索旋转排序数组

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">  


## Description - 题目描述

### EN:
<p>There is an integer array <code>nums</code> sorted in ascending order (with <strong>distinct</strong> values).</p>

<p>Prior to being passed to your function, <code>nums</code> is <strong>possibly rotated</strong> at an unknown pivot index <code>k</code> (<code>1 &lt;= k &lt; nums.length</code>) such that the resulting array is <code>[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]</code> (<strong>0-indexed</strong>). For example, <code>[0,1,2,4,5,6,7]</code> might be rotated at pivot index <code>3</code> and become <code>[4,5,6,7,0,1,2]</code>.</p>

<p>Given the array <code>nums</code> <strong>after</strong> the possible rotation and an integer <code>target</code>, return <em>the index of </em><code>target</code><em> if it is in </em><code>nums</code><em>, or </em><code>-1</code><em> if it is not in </em><code>nums</code>.</p>

<p>You must write an algorithm with <code>O(log n)</code> runtime complexity.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [4,5,6,7,0,1,2], target = 0
<strong>Output:</strong> 4
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [4,5,6,7,0,1,2], target = 3
<strong>Output:</strong> -1
</pre><p><strong>Example 3:</strong></p>
<pre><strong>Input:</strong> nums = [1], target = 0
<strong>Output:</strong> -1
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 5000</code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li>All values of <code>nums</code> are <strong>unique</strong>.</li>
	<li><code>nums</code> is an ascending array that is possibly rotated.</li>
	<li><code>-10<sup>4</sup> &lt;= target &lt;= 10<sup>4</sup></code></li>
</ul>


### ZH-CN:
<p>整数数组 <code>nums</code> 按升序排列，数组中的值 <strong>互不相同</strong> 。</p>

<p>在传递给函数之前，<code>nums</code> 在预先未知的某个下标 <code>k</code>（<code>0 <= k < nums.length</code>）上进行了 <strong>旋转</strong>，使数组变为 <code>[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]</code>（下标 <strong>从 0 开始</strong> 计数）。例如， <code>[0,1,2,4,5,6,7]</code> 在下标 <code>3</code> 处经旋转后可能变为 <code>[4,5,6,7,0,1,2]</code> 。</p>

<p>给你 <strong>旋转后</strong> 的数组 <code>nums</code> 和一个整数 <code>target</code> ，如果 <code>nums</code> 中存在这个目标值 <code>target</code> ，则返回它的下标，否则返回 <code>-1</code> 。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [<code>4,5,6,7,0,1,2]</code>, target = 0
<strong>输出：</strong>4
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [<code>4,5,6,7,0,1,2]</code>, target = 3
<strong>输出：</strong>-1</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>nums = [1], target = 0
<strong>输出：</strong>-1
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 <= nums.length <= 5000</code></li>
	<li><code>-10^4 <= nums[i] <= 10^4</code></li>
	<li><code>nums</code> 中的每个值都 <strong>独一无二</strong></li>
	<li>题目数据保证 <code>nums</code> 在预先未知的某个下标上进行了旋转</li>
	<li><code>-10^4 <= target <= 10^4</code></li>
</ul>

<p> </p>

<p><strong>进阶：</strong>你可以设计一个时间复杂度为 <code>O(log n)</code> 的解决方案吗？</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 0 ms | 10.9 MB | 2021/03/30 14:01 |

```cpp

/*
如何得到思路：
直接顺序查找时间复杂度为O(N)
题目要求时间复杂度为O(logN),自然想到要用二分

思路：
实际上还是二分查找的步骤。只不过修改二分查找的上下界的判断方式变了。

对于有序数组，可以使用二分查找的方法查找元素。
但是这道题中，数组本身不是有序的，进行旋转后只保证了数组的局部是有序的，这还能进行二分查找吗？答案是可以的。
可以发现的是，我们将数组从中间分开成左右两部分的时候，一定有一部分的数组是有序的，而另一部分可能有序也可能无序(局部有序)。

这启示我们可以在常规二分查找的时候检查 [left, mid] 和 [mid + 1, right] 哪个部分是有序的，**并根据有序的那个部分确定我们该如何改变二分查找的上下界**，因为我们能够根据有序的那部分判断出 target 在不在这个部分。
(完全有序数组的二分查找，则是根据和mid的比较)

如果target==nums[mid],则返回mid; 
如果 [left, mid - 1] 是有序数组，且 target 的大小位于 [nums[0],nums[mid])区间内，则我们应该将搜索范围缩小至 [l, mid - 1]，否则在 [mid + 1, right] 中寻找。
如果 [mid, right] 是有序数组，且 target 的大小满足(nums[mid+1],nums[nums.size()-1]]，则我们应该将搜索范围缩小至 [mid + 1, right]，否则在 [left, mid - 1] 中寻找。

*/
class Solution {
public:
    int search(vector<int>& nums, int target) {
        /*变量定义及初始化*/
        int n=nums.size();
        int left=0,right=n-1;
        int mid=0;

        /*算法主体*/
        //处理特例
        if(n==0)
            return -1;
        if(n==1)
            return nums[0]==target ? 0 : -1;

        //一般情况
        while(left<=right){
            mid=(left+right)/2;//找当前操作区间中点

            if(nums[mid]==target)//找到目标元素
                return mid;
            
            if(nums[0]<=nums[mid]){//左半段为有序部分，利用这一性质确定接下来区间的取舍(选左半段还是右半段)
                if(nums[0]<=target && target<nums[mid])//目标元素在左半段，接下来选左半段接着进行二分
                    right=mid-1;
                else//目标元素在右半段
                    left=mid+1;
            }
            else{//右半段为有序部分
                if(nums[mid]<target && target<=nums[n-1] )//目标元素在右半段
                    left=mid+1;
                else//目标元素在左半段
                    right=mid-1;
            }
        }

        /*返回结果*/
        return -1;//没找到

    }
};

```
## My Notes - 我的笔记


No notes

