
# 151. Reverse Words in a String - 颠倒字符串中的单词

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">  


## Description - 题目描述

### EN:
<p>Given an input string <code>s</code>, reverse the order of the <strong>words</strong>.</p>

<p>A <strong>word</strong> is defined as a sequence of non-space characters. The <strong>words</strong> in <code>s</code> will be separated by at least one space.</p>

<p>Return <em>a string of the words in reverse order concatenated by a single space.</em></p>

<p><b>Note</b> that <code>s</code> may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;the sky is blue&quot;
<strong>Output:</strong> &quot;blue is sky the&quot;
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;  hello world  &quot;
<strong>Output:</strong> &quot;world hello&quot;
<strong>Explanation:</strong> Your reversed string should not contain leading or trailing spaces.
</pre>

<p><strong>Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;a good   example&quot;
<strong>Output:</strong> &quot;example good a&quot;
<strong>Explanation:</strong> You need to reduce multiple spaces between two words to a single space in the reversed string.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>4</sup></code></li>
	<li><code>s</code> contains English letters (upper-case and lower-case), digits, and spaces <code>&#39; &#39;</code>.</li>
	<li>There is <strong>at least one</strong> word in <code>s</code>.</li>
</ul>

<p>&nbsp;</p>
<p><b data-stringify-type="bold">Follow-up:&nbsp;</b>If the string data type is mutable in your language, can&nbsp;you solve it&nbsp;<b data-stringify-type="bold">in-place</b>&nbsp;with&nbsp;<code data-stringify-type="code">O(1)</code>&nbsp;extra space?</p>


### ZH-CN:
<p>给你一个字符串 <code>s</code> ，颠倒字符串中 <strong>单词</strong> 的顺序。</p>

<p><strong>单词</strong> 是由非空格字符组成的字符串。<code>s</code> 中使用至少一个空格将字符串中的 <strong>单词</strong> 分隔开。</p>

<p>返回 <strong>单词</strong> 顺序颠倒且 <strong>单词</strong> 之间用单个空格连接的结果字符串。</p>

<p><strong>注意：</strong>输入字符串 <code>s</code>中可能会存在前导空格、尾随空格或者单词间的多个空格。返回的结果字符串中，单词间应当仅用单个空格分隔，且不包含任何额外的空格。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>s = "<code>the sky is blue</code>"
<strong>输出：</strong>"<code>blue is sky the</code>"
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>s = " &nbsp;hello world &nbsp;"
<strong>输出：</strong>"world hello"
<strong>解释：</strong>颠倒后的字符串中不能存在前导空格和尾随空格。
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>s = "a good &nbsp; example"
<strong>输出：</strong>"example good a"
<strong>解释：</strong>如果两个单词间有多余的空格，颠倒后的字符串需要将单词间的空格减少到仅有一个。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>4</sup></code></li>
	<li><code>s</code> 包含英文大小写字母、数字和空格 <code>' '</code></li>
	<li><code>s</code> 中 <strong>至少存在一个</strong> 单词</li>
</ul>

<ul>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>如果字符串在你使用的编程语言中是一种可变数据类型，请尝试使用&nbsp;<code>O(1)</code> 额外空间复杂度的 <strong>原地</strong> 解法。</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/reverse-words-in-a-string/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/reverse-words-in-a-string/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 4 ms | 6.9 MB | 2021/03/28 13:18 |

```cpp

/*
1. 先对整个字符串进行翻转 "this is" -> "si siht"
2. 再分别对各个单词进行翻转 "si siht" -> "is this"
  2.1 先将当前单词前移，覆盖掉前面多余的空格
  2.2 再对当前单词进行翻转 (调用 `reverse()` 函数)
  2.3 擦除后面多余的内容 (调用`s.erase()` 函数)
*/
class Solution {
public:
    string reverseWords(string s) {
        /*变量定义及初始化*/
        int start=0;//整个字符串的扫描指针
        int end=0;//当前单词的扫描指针
        int i=0;//当前单词前移后的位置的扫描指针
        int len=0;//当前单词的长度

        /*算法主体*/
        //1. 对整个字符串进行翻转
        reverse(s.begin(),s.end());

        //2. 对各个单词分别进行翻转(先前移覆盖掉前面多余的空格，再翻转)
        while(start<s.size()){
            //找到当前单词的起始字符
            if(s[start]!=' '){
                //如果当前i指向的位置不是第一个单词的起始字符，则添加空格，并将i移动到下一个位置
                if(i!=0)
                    s[i++]=' ';
                
                //遍历当前单词，将其前移后翻转
                end=start;
                
                //2.1 将单词前移
                while(s[end]!=' ' && end<s.size())
                    s[i++]=s[end++];
                
                //2.2 将前移后的单词翻转
                len=end-start;//单词长度
                reverse(s.begin()+i-len,s.begin()+i);

                start=end;//start跳到当前单词结尾的下一个位置，以接着寻找下一个单词

            }      
            //start接着往下遍历
            start++;
        }
        //2.3 将后面多余的内容删掉(空格、前移后的单词前移前的内容)
        s.erase(s.begin()+i,s.end());
        /*返回结果*/
        return s;
    }
};

```
## My Notes - 我的笔记


No notes

