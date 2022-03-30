
# 4. Median of Two Sorted Arrays - 寻找两个正序数组的中位数

## Tags - 题目标签

 <img src="https://img.shields.io/badge/Array-数组-blue.svg">   <img src="https://img.shields.io/badge/Binary Search-二分查找-blue.svg">   <img src="https://img.shields.io/badge/Divide and Conquer-分治-blue.svg">  


## Description - 题目描述

### EN:
<p>Given two sorted arrays <code>nums1</code> and <code>nums2</code> of size <code>m</code> and <code>n</code> respectively, return <strong>the median</strong> of the two sorted arrays.</p>

<p>The overall run time complexity should be <code>O(log (m+n))</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [1,3], nums2 = [2]
<strong>Output:</strong> 2.00000
<strong>Explanation:</strong> merged array = [1,2,3] and median is 2.
</pre>

<p><strong>Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [1,2], nums2 = [3,4]
<strong>Output:</strong> 2.50000
<strong>Explanation:</strong> merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>nums1.length == m</code></li>
	<li><code>nums2.length == n</code></li>
	<li><code>0 &lt;= m &lt;= 1000</code></li>
	<li><code>0 &lt;= n &lt;= 1000</code></li>
	<li><code>1 &lt;= m + n &lt;= 2000</code></li>
	<li><code>-10<sup>6</sup> &lt;= nums1[i], nums2[i] &lt;= 10<sup>6</sup></code></li>
</ul>


### ZH-CN:
<p>给定两个大小分别为 <code>m</code> 和 <code>n</code> 的正序（从小到大）数组&nbsp;<code>nums1</code> 和&nbsp;<code>nums2</code>。请你找出并返回这两个正序数组的 <strong>中位数</strong> 。</p>

<p>算法的时间复杂度应该为 <code>O(log (m+n))</code> 。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>nums1 = [1,3], nums2 = [2]
<strong>输出：</strong>2.00000
<strong>解释：</strong>合并数组 = [1,2,3] ，中位数 2
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>nums1 = [1,2], nums2 = [3,4]
<strong>输出：</strong>2.50000
<strong>解释：</strong>合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
</pre>

<p>&nbsp;</p>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>nums1.length == m</code></li>
	<li><code>nums2.length == n</code></li>
	<li><code>0 &lt;= m &lt;= 1000</code></li>
	<li><code>0 &lt;= n &lt;= 1000</code></li>
	<li><code>1 &lt;= m + n &lt;= 2000</code></li>
	<li><code>-10<sup>6</sup> &lt;= nums1[i], nums2[i] &lt;= 10<sup>6</sup></code></li>
</ul>



## Link - 题目链接

[LeetCode](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)  -  [LeetCode-CN](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/description/)
## Latest Accepted Submissions - 最近一次 AC 的提交


| Language | Runtime | Memory | Submission Time |
|:---:|:---:|:---:|:---:|
| cpp  | 48 ms | 86.8 MB | 2021/03/29 11:15 |

```cpp

/*
主函数：
- 如果两个数组总长度是奇数，则中位数就是中间那个数(第(totalLength + 1)/2小)
- 如果两个数组总长度是偶数，则中位数是中间的两个数的平均值(第totalLength/2小 和 第totalLength/2+1的平均值)

找第k小的函数：
- 要找到第 k (k>1) 小的元素，那么就取 pivot1 = nums1[k/2-1] 和 pivot2 = nums2[k/2-1] 进行比较
- nums1 中小于等于 pivot1 的元素有 nums1[0 .. k/2-2] 共计 k/2-1 个;
- nums2 中小于等于 pivot2 的元素有 nums2[0 .. k/2-2] 共计 k/2-1 个
- 取 pivot = min(pivot1, pivot2)，两个数组中小于等于 pivot 的元素共计不会超过 (k/2-1) + (k/2-1) <= k-2 个
- 这样 pivot 本身最大也只能是第 k-1 小的元素
- 如果 pivot = pivot1，那么 nums1[0 .. k/2-1] 都不可能是第 k 小的元素。把这些元素全部 "砍"掉，剩下的作为新的 nums1 数组
- 如果 pivot = pivot2，那么 nums2[0 .. k/2-1] 都不可能是第 k 小的元素。把这些元素全部 "砍"掉，剩下的作为新的 nums2 数组
- 由于我们 "砍"掉了一些元素（这些元素都比第 k 小的元素要小），因此需要修改 k 的值，减去砍掉的数的个数。
- 比如原先要找第k小，去掉s个比目标数小的数后，变成在新数组找第k-s小
*/
class Solution {
public:
    /*找第k小的函数*/
    double getKthElement(vector<int>& nums1,vector<int>& nums2,int k){//找有序数组nums1和nums2的合并后的第k小
        /*变量定义与初始化*/
        int len1=nums1.size(),len2=nums2.size();//两个数组的长度
        int index1=0,index2=0;//两个数组当前操作区域的起始下标
        int pivotIndex1=0,pivotIndex2=0;//两个数组pivot元素的下标
        int pivot1=0,pivot2=0;//两个数组的pivot值

        /*算法主体*/
        while(true){
            /*返回结果(出口条件)*/
            if(index1==len1) //nums1数组被砍完了，此时nums2被砍了index2(该值为最新值，可能为0)
                return nums2[k+index2-1];
                //假设初始时传入的k的值为K。此时应该返回nums2数组的第K-len1小，即下标为K-len1-1的元素。
                //而现在最新的k值为K-len1-index2,将其待入，即应该返回nums2中下标为k+index2-1的元素。
            
            if(index2==len2)//num2数组被砍完了
                return nums1[k+index1-1];
            
            if(k==1) // 如果在nums1和nums2被砍完之前,k的值被更新为1，则进行以下运算会出错(更新pivotIndex1时k/2=0，导致其后退)，所以需要单独处理
                return min(nums1[index1],nums2[index2]);//要找当前操作区域的第1小

            /*操作主体(一般情况))*/
            //不断砍去数组，更新当前操作区域的pivot下标、pivot值，k,起始下标
            pivotIndex1=min(index1+k/2-1,len1-1);//更新nums1的当前操作区域的pivot下标。本意是取index1+k/2-1，但若该值越界，则取边界值
            pivotIndex2=min(index2+k/2-1,len2-1);//min()函数表示取两个参数中的较小者
            pivot1=nums1[pivotIndex1];
            pivot2=nums2[pivotIndex2];

            if(pivot1<=pivot2){//砍nums1数组的
                k-=(pivotIndex1-index1+1);//更新k。减去被砍掉的数，包括nums1数组中pivotIndex1至index1之间的数及pivotIndex对应的数本身
                index1=pivotIndex1+1;//更新nums1当前操作区域起始下标。砍掉pivotIndex1前面及其本身的数
            }
            else{
                k-=(pivotIndex2-index2+1);
                index2=pivotIndex2+1;
            }

        }
    }

    /*主函数*/
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int totalLen=nums1.size()+nums2.size();
        if((totalLen)%2==1)//总长度为奇数，中位数就是总数组中间那个数
            return getKthElement(nums1,nums2,(totalLen+1)/2);
        else//中位数是总数组中间那两个数的平均值
            return (getKthElement(nums1,nums2,totalLen/2)+getKthElement(nums1,nums2,totalLen/2+1)) / 2.0;

    }
};

```
## My Notes - 我的笔记


No notes

