
# 剑指 Offer 58 - I. 翻转单词顺序 LCOF - 翻转单词顺序

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Two Pointers-双指针-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">  


## Description - 题目描述

### EN:
<p>English description is not available for the problem. Please switch to Chinese.</p>

### ZH-CN:
<p>输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串&quot;I am a student. &quot;，则输出&quot;student. a am I&quot;。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入:</strong> &quot;<code>the sky is blue</code>&quot;
<strong>输出:&nbsp;</strong>&quot;<code>blue is sky the</code>&quot;
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入:</strong> &quot; &nbsp;hello world! &nbsp;&quot;
<strong>输出:&nbsp;</strong>&quot;world! hello&quot;
<strong>解释: </strong>输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
</pre>

<p><strong>示例 3：</strong></p>

<pre><strong>输入:</strong> &quot;a good &nbsp; example&quot;
<strong>输出:&nbsp;</strong>&quot;example good a&quot;
<strong>解释: </strong>如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
</pre>

<p>&nbsp;</p>

<p><strong>说明：</strong></p>

<ul>
	<li>无空格字符构成一个单词。</li>
	<li>输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。</li>
	<li>如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。</li>
</ul>

<p><strong>注意：</strong>本题与主站 151 题相同：<a href="https://leetcode-cn.com/problems/reverse-words-in-a-string/">https://leetcode-cn.com/problems/reverse-words-in-a-string/</a></p>

<p><strong>注意：</strong>此题对比原题有改动</p>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 4 ms | 7 MB | 2021/03/28 13:18 |

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

