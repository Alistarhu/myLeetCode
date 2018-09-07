# 90. Subsets II - Medium

## Description
Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

## Example
```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

## Analysis
这道题需要求一个包含重复元素集合的所有子集。**由于集合中包含有重复元素，因此需要在生成子集的过程中过滤到重复的解。**

这道题采用回溯方法，逐层向下递归，**为了消除重复解，在每一轮中同一个位置上的重复元素只能被使用一次！**

下面举例说明如何去重，集合`[1,2,2,3]`
- 长度为0的子集有1个
- 长度为1的子集有三种可能：1、2、3。这里的两个`2`能出现一次，这两个2位于同一个位置上;
- 长度为2的子集是在长度为1的子集的基础之上生成的，注意这里`22`是符合要求的，应为这两个2位于不同的位置上，“所承担的价值不同”。
- 消除重复关键在于条件 `i!=start_idx && nums[i]==nums[i-1]`

## Solution
```c++
class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> curset;
        res.push_back(curset);
        if(nums.size()!=0)
            sort(nums.begin(),nums.end());
        backtrack(res, curset, 0, nums);
        return res;
    }

    void backtrack(vector<vector<int>>& res, vector<int>& curset, int start_idx, vector<int> nums)
    {
        if(curset.size()!=0)
            res.push_back(curset);
        for(int i=start_idx;i<nums.size();i++)
        {
            if(i==0)
            {
                curset.push_back(nums[i]);
                backtrack(res, curset, i+1, nums);// find the next position num
                curset.pop_back();
            }
            else if(i!=start_idx&&nums[i]==nums[i-1])//filter the same nums of the same position!!!!!
                continue;
            else
            {
                curset.push_back(nums[i]);
                backtrack(res, curset, i+1, nums);
                curset.pop_back();
            }
        }
    }
};
```
