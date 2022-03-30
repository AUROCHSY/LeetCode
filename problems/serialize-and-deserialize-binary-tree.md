
# 297. Serialize and Deserialize Binary Tree - 二叉树的序列化与反序列化

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Tree-树-blue.svg">   <img src="https://img.shields.io/badge/Depth-First Search-深度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Breadth-First Search-广度优先搜索-blue.svg">   <img src="https://img.shields.io/badge/Design-设计-blue.svg">   <img src="https://img.shields.io/badge/String-字符串-blue.svg">   <img src="https://img.shields.io/badge/Binary Tree-二叉树-blue.svg">  


## Description - 题目描述

### EN:
<p>Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.</p>

<p>Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.</p>

<p><strong>Clarification:</strong> The input/output format is the same as <a href="/faq/#binary-tree" target="_blank">how LeetCode serializes a binary tree</a>. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg" style="width: 442px; height: 324px;" />
<pre>
<strong>Input:</strong> root = [1,2,3,null,null,4,5]
<strong>Output:</strong> [1,2,3,null,null,4,5]
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 10<sup>4</sup>]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
</ul>


### ZH-CN:
<p>序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。</p>

<p>请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。</p>

<p><strong>提示: </strong>输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 <a href="/faq/#binary-tree">LeetCode 序列化二叉树的格式</a>。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。</p>

<p> </p>

<p><strong>示例 1：</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg" style="width: 442px; height: 324px;" />
<pre>
<strong>输入：</strong>root = [1,2,3,null,null,4,5]
<strong>输出：</strong>[1,2,3,null,null,4,5]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>root = []
<strong>输出：</strong>[]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>root = [1]
<strong>输出：</strong>[1]
</pre>

<p><strong>示例 4：</strong></p>

<pre>
<strong>输入：</strong>root = [1,2]
<strong>输出：</strong>[1,2]
</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li>树中结点数在范围 <code>[0, 10<sup>4</sup>]</code> 内</li>
	<li><code>-1000 <= Node.val <= 1000</code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 56 ms | 32.8 MB | 2021/04/07 15:24 |

```cpp

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

class Codec {
public:
    /*全局变量定义*/
    string NULLTAG = "#"; //空节点的标记
    string SEP = ","; //节点之间的分隔符
    string res; //用于记录二叉树序列化结果字符串
    queue<string> treeQueue; //用于保存二叉树字符串转换成的队列

    /***序列化二叉树***/
    /*主函数：
    输入：待处理二叉树根节点
    输出：二叉树序列化结果字符串
    操作：调用dfs()函数将二叉树序列化，return返回结果
    */
    string serialize(TreeNode* root) {
        dfs(root);
        return res;
    }

    /*辅助函数：用深度优先(前序遍历)的方式序列化二叉树,也可以用后序遍历或层序遍历
    输入：当前待处理二叉树的根节点
    输出：无直接return输出。通过修改全局变量res间接输出
    操作：用前序遍历的方式序列化二叉树为字符串
    */
    void dfs(TreeNode* root){
        /*递归出口*/    
        //* 第一层特例处理出口 & 最深层调用返回出口
        if (!root){ //空节点存入标记NULLTAG 及 分隔符SEP
            res += NULLTAG + SEP;
            return;
        }              

        /*本层处理*/    
        res += to_string(root->val) + SEP;  //非空节点存入节点值和分割符
        
        /*递归调用*/
        dfs(root->left);                    
        dfs(root->right);                   

    }

    //反序列化阶段
    TreeNode* deserialize(string treeStr) {        
        
        split(treeStr);//将二叉树序列化结果字符串进行分割，节点信息存入队列tree(全局变量)
        //用双指针扫描法，按照逗号来分割字符串，得到子树序列队列
        return de_dfs();                        //递归建树
    }

    //仍然用前序遍历的方式，从二叉树数组中构建二叉树
    TreeNode* de_dfs(){
        auto t = treeQueue.front();
        treeQueue.pop();

        if (t == NULLTAG) return nullptr;

        TreeNode* root = new TreeNode(stoi(t)); //stoi()函数将 string 转为 int
        root->left = de_dfs();
        root->right = de_dfs();

        return root;
    }
    /*字符串分割函数：C++没有自带的字符串分割函数，需要自己实现
    输入：字符串
    输出：无直接return输出，通过修改全局变量treeQueue输出
    操作：
    */
    void split(string treeStr){
        int i = 0, j = 0; //i是扫描指针，j指向欲取出子串的起始位置
        //将string类型的分隔符转为const char*类型(字符串转为char数组),使用时要用取值符号*sep                      
        const char *sep = SEP.c_str();//将"," 转为',' 如果在定义时就定义为char, 则在拼接字符串时需要将其转为string
        while (i < treeStr.size()){     
            while (treeStr[i] != *sep && i < treeStr.size()) 
                i++;
            string tmp = treeStr.substr(j, i - j); //取出分隔符之间的内容
            treeQueue.push(tmp);
            i++ ;
            j=i;
        }
    }
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));

```
## My Notes - 我的笔记


No notes

