
# 322. Coin Change - 零钱兑换

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Breadth-First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>You are given an integer array <code>coins</code> representing coins of different denominations and an integer <code>amount</code> representing a total amount of money.</p>

<p>Return <em>the fewest number of coins that you need to make up that amount</em>. If that amount of money cannot be made up by any combination of the coins, return <code>-1</code>.</p>

<p>You may assume that you have an infinite number of each kind of coin.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> coins = [1,2,5], amount = 11
<strong>Output:</strong> 3
<strong>Explanation:</strong> 11 = 5 + 5 + 1
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> coins = [2], amount = 3
<strong>Output:</strong> -1
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> coins = [1], amount = 0
<strong>Output:</strong> 0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= coins.length &lt;= 12</code></li>
	<li><code>1 &lt;= coins[i] &lt;= 2<sup>31</sup> - 1</code></li>
	<li><code>0 &lt;= amount &lt;= 10<sup>4</sup></code></li>
</ul>


### ZH-CN:
<p>给你一个整数数组 <code>coins</code> ，表示不同面额的硬币；以及一个整数 <code>amount</code> ，表示总金额。</p>

<p>计算并返回可以凑成总金额所需的 <strong>最少的硬币个数</strong> 。如果没有任何一种硬币组合能组成总金额，返回&nbsp;<code>-1</code> 。</p>

<p>你可以认为每种硬币的数量是无限的。</p>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1：</strong></p>

<pre>
<strong>输入：</strong>coins = <code>[1, 2, 5]</code>, amount = <code>11</code>
<strong>输出：</strong><code>3</code> 
<strong>解释：</strong>11 = 5 + 5 + 1</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>coins = <code>[2]</code>, amount = <code>3</code>
<strong>输出：</strong>-1</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>coins = [1], amount = 0
<strong>输出：</strong>0
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= coins.length &lt;= 12</code></li>
	<li><code>1 &lt;= coins[i] &lt;= 2<sup>31</sup> - 1</code></li>
	<li><code>0 &lt;= amount &lt;= 10<sup>4</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/coin-change/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/coin-change/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 84 ms | 14.2 MB | 2021/04/10 11:26 |

```cpp

class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        /*变量声明及初始化*/
        //dp[amount]表示总额为amount所需的硬币数
        vector<int> dp(amount+1,amount+1);//数组大小为amount+1,数组值最大能取amount,所以初始化为amount+1相当于初始化为无穷大

        /*算法主体*/
        //*特例 base case
        dp[0]=0; //其它情况计算的基础，很重要，别遗漏了

        //*计算其它情况
        //计算总金额为0到 amount 的情况
        for(int i=0;i<dp.size();i++){ 
            
            //coin的面值有{1,2,5},此循环通过两两比较的方式比较 dp[i],dp[i-1]+1,dp[i-3]+1,dp[i-5]+1
            for(int coin : coins){ 
                //子问题总金额小于0, 此种情况不存在, 此次比较跳过
                if(i-coin<0)
                    continue;
                //自顶向下,利用子问题的最优解求当前问题最优解
                dp[i] = min(dp[i],dp[i-coin] + 1);//+1表示子问题的最优解再加1个硬币
            }
        }

        /*返回结果*/
        return (dp[amount]==amount+1) ? -1: dp[amount];

    }
};

```
## My Notes - 我的笔记


No notes

