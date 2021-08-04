# [152. Maximum Product Subarray](https://leetcode-cn.com/problems/maximum-product-subarray/)
## 题目
Given an integer array nums, find a contiguous non-empty subarray within the array that has the largest product, and return the product. 

It is guaranteed that the answer will fit in a 32-bit integer. 

A subarray is a contiguous subsequence of the array.

Example 1:
```
Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```
## 解题思路
动态规划，用maxn, minn记录以第i个元素结尾的子数组的乘积最大最小值，很容易推导出状态转移方程

![](https://latex.codecogs.com/svg.latex?maxn=max(maxn*nums[i],max(minn*nums[i],nums[i])))

![](https://latex.codecogs.com/svg.latex?minn=min(minn*nums[i],min(maxn*nums[i],nums[i])))

## 代码
```C++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int maxN = 1, minN = 1;
        int res = nums[0], n = nums.size();
        for(int i = 0; i < n; ++i)
        {
            int tmp1 = maxN * nums[i], tmp2 = minN * nums[i];
            maxN = max(max(tmp1, tmp2), nums[i]);
            minN = min(min(tmp1, tmp2), nums[i]);
            res = max(res, maxN);
        }
        return res;
    }
};
```

