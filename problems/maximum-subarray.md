
# 53. Maximum Subarray - 最大子数组和

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an integer array <code>nums</code>, find the contiguous subarray (containing at least one number) which has the largest sum and return <em>its sum</em>.</p>

<p>A <strong>subarray</strong> is a <strong>contiguous</strong> part of an array.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [-2,1,-3,4,-1,2,1,-5,4]
<strong>Output:</strong> 6
<strong>Explanation:</strong> [4,-1,2,1] has the largest sum = 6.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1]
<strong>Output:</strong> 1
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [5,4,-1,7,8]
<strong>Output:</strong> 23
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> If you have figured out the <code>O(n)</code> solution, try coding another solution using the <strong>divide and conquer</strong> approach, which is more subtle.</p>


### ZH-CN:
<p>给你一个整数数组 <code>nums</code> ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。</p>

<p><strong>子数组 </strong>是数组中的一个连续部分。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums = [-2,1,-3,4,-1,2,1,-5,4]
<strong>输出：</strong>6
<strong>解释：</strong>连续子数组&nbsp;[4,-1,2,1] 的和最大，为&nbsp;6 。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums = [1]
<strong>输出：</strong>1
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>nums = [5,4,-1,7,8]
<strong>输出：</strong>23
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>如果你已经实现复杂度为 <code>O(n)</code> 的解法，尝试使用更为精妙的 <strong>分治法</strong> 求解。</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/maximum-subarray/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/maximum-subarray/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 12 ms | 12.8 MB | 2021/04/12 9:08 |

```cpp

class Solution {
public:
    /*进行了状态压缩，时间复杂度为O(n)，空间复杂度为O(1)*/
    int maxSubArray(vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return 0;

    // base case
    int dp_0 = nums[0]; //存储上一层状态
    int dp_1 = 0; //存储当前状态
    int res = dp_0; //存储结果

    for (int i = 1; i < n; i++) {
        dp_1 = max(nums[i],dp_0 + nums[i]);//当前状态

        dp_0 = dp_1; //将当前状态赋值给存储`上一状态`的变量，进入下一轮循环

        res = max(res, dp_1);// 更新结果。比较之前得到的res和当前状态
    }

    return res;
}

    /*未进行状态压缩：时间复杂度为O(n)，空间复杂度为O(n)*/
    // int maxSubArray(vector<int>& nums) {
    //     /*1.变量声明及初始化*/
    //     int n = nums.size();
    //     vector<int> dp(n);//dp[i]: 以 nums[i] 为结尾的 最大子数组和

    //     /*2.算法主体*/
    //     //*2.1特例处理
    //     //-异常输入
    //     if (n == 0) return 0;
    //     //-base case:第一个元素前面没有子数组,其最大子数组和就是它本身
    //     dp[0] = nums[0];

    //     //*2.2一般情况：状态转移方程
    //     //计算各个位置的 最大子数组和
    //     for (int i = 1; i < n; i++) {
    //         dp[i] = max(nums[i], dp[i - 1] + nums[i]);
    //     }

    //     //取 nums[] 的最大元素值即为整个输入数组的最大子数组
    //     int res = INT_MIN;
    //     for (int i = 0; i < n; i++) {
    //         res = max(res, dp[i]);
    //     }
    //     return res;
    // }
};

```
## My Notes - 我的笔记


No notes

