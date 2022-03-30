
# 72. Edit Distance - 编辑距离

## Tags - 题目标签

 <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Dynamic Programming-动态规划-blue.svg">  


## Description - 题目描述

### EN:
<p>Given two strings <code>word1</code> and <code>word2</code>, return <em>the minimum number of operations required to convert <code>word1</code> to <code>word2</code></em>.</p>

<p>You have the following three operations permitted on a word:</p>

<ul>
	<li>Insert a character</li>
	<li>Delete a character</li>
	<li>Replace a character</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> word1 = &quot;horse&quot;, word2 = &quot;ros&quot;
<strong>Output:</strong> 3
<strong>Explanation:</strong> 
horse -&gt; rorse (replace &#39;h&#39; with &#39;r&#39;)
rorse -&gt; rose (remove &#39;r&#39;)
rose -&gt; ros (remove &#39;e&#39;)
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> word1 = &quot;intention&quot;, word2 = &quot;execution&quot;
<strong>Output:</strong> 5
<strong>Explanation:</strong> 
intention -&gt; inention (remove &#39;t&#39;)
inention -&gt; enention (replace &#39;i&#39; with &#39;e&#39;)
enention -&gt; exention (replace &#39;n&#39; with &#39;x&#39;)
exention -&gt; exection (replace &#39;n&#39; with &#39;c&#39;)
exection -&gt; execution (insert &#39;u&#39;)
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= word1.length, word2.length &lt;= 500</code></li>
	<li><code>word1</code> and <code>word2</code> consist of lowercase English letters.</li>
</ul>


### ZH-CN:
<p>给你两个单词&nbsp;<code>word1</code> 和&nbsp;<code>word2</code>， <em>请返回将&nbsp;<code>word1</code>&nbsp;转换成&nbsp;<code>word2</code> 所使用的最少操作数</em> &nbsp;。</p>

<p>你可以对一个单词进行如下三种操作：</p>

<ul>
	<li>插入一个字符</li>
	<li>删除一个字符</li>
	<li>替换一个字符</li>
</ul>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1：</strong></p>

<pre>
<strong>输入：</strong>word1 = "horse", word2 = "ros"
<strong>输出：</strong>3
<strong>解释：</strong>
horse -&gt; rorse (将 'h' 替换为 'r')
rorse -&gt; rose (删除 'r')
rose -&gt; ros (删除 'e')
</pre>

<p><strong>示例&nbsp;2：</strong></p>

<pre>
<strong>输入：</strong>word1 = "intention", word2 = "execution"
<strong>输出：</strong>5
<strong>解释：</strong>
intention -&gt; inention (删除 't')
inention -&gt; enention (将 'i' 替换为 'e')
enention -&gt; exention (将 'n' 替换为 'x')
exention -&gt; exection (将 'n' 替换为 'c')
exection -&gt; execution (插入 'u')
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>0 &lt;= word1.length, word2.length &lt;= 500</code></li>
	<li><code>word1</code> 和 <code>word2</code> 由小写英文字母组成</li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/edit-distance/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/edit-distance/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 4 ms | 7.1 MB | 2021/04/11 17:14 |

```cpp

class Solution {
public:
    int minDistance(string s1, string s2) {//s1为待处理串，s2为匹配目标串
        /*变量声明及初始化*/
        int m=s1.size(),n=s2.size();
        int dp[m+1][n+1];
        memset(dp,0,sizeof(dp));

        /*算法主体*/
        //*base case特例处理：base case 就是i遍历完后 或者 j遍历完后，此时直接返回剩余字符串的字符个数即为仍需要进行的操作个数
        for(int i=1;i<=m;i++)
            dp[i][0]=i; //s2遍历完了，其遍历指针 j 到达第一个字符的前一个位置
        for(int j=1;j<=n;j++)
            dp[0][j]=j;//s1遍历完了，其遍历指针 j 到达第一个字符的前一个位置

        //*一般情况处理
        for(int i=1;i<=m;i++){
            for(int j=1;j<=n;j++){
                if(s1[i-1]==s2[j-1]) //比较s1的第i个,s2的第j个字符，其下标为序号-1
                    dp[i][j]=dp[i-1][j-1]; //当前比较字符相等，无需操作，直接进行下一位的比较
                else{//不匹配，则可进行删除、插入或替换操作,这三种操作都需要将操作数+1,取三者中的操作数最小者作为dp[i][j]的值
                    dp[i][j]=getMin( 
                        dp[i-1][j]+1, //插入,i向前移一位，操作数+1
                        dp[i][j-1]+1, //删除，j向前移一位，操作数+1
                        dp[i-1][j-1]+1 //替换，i j都向前移一位，操作数+1
                    );

                }
            }
        }
        /*返回结果*/
        return dp[m][n];
    }

/*求三个数的最小值函数*/
    int getMin(int a, int b, int c){
        return min(a,min(b,c));
    }

};

```
## My Notes - 我的笔记


No notes

