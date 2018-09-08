# 91. Decode Ways - Medium

## Description
A message containing letters from A-Z is being encoded to numbers using the following mapping:
```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```
Given a non-empty string containing only digits, determine the total number of ways to decode it.

## Example
```
Example 1:
Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).

Example 2:
Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

## Analysis
这道题是一道考察动态规划问题，主要看这串数字共有多少种拆分的可能。

原问题可以分解成为子问题进行求解，递推关系：
- 如果前两个数字能够组合成为一个符合要求的两位数，那么：拆分的情况数=后n-1个数的拆分数+后n-2个数的拆分数
- 如果前两个数字能不够组合成为一个符合要求的两位数，且前一个数字大于0，那么：拆分的情况数=后n-1个数的拆分数
- 如果前两个数字能不够组合成为一个符合要求的两位数，且前一个数字为0，那么：拆分的情况数=0

从字面意思上看很像是递归的做法， **但直接递归会造成重复计算，这里使用动态规划思想采用由底向上正向的进行求解**，由最后一个元素为起点，逐次向前添加元素，计算每个长度下的拆分方法数，最终可以得到长度为n的拆分方法数目。

## Solution
```c++
class Solution {
public:
    int numDecodings(string s) {
        int len=s.size();
        vector<int> dp(len+1,0);
        // init
        dp[len]=1;
        if(s[len-1]!='0')
            dp[len-1]=1;

        for(int i=len-2;i>=0;i--)
        {
            if(s[i]=='0')
                dp[i]=0;
            else
            {
                if((s[i]-'0')*10+s[i+1]-'0'<=26)
                    dp[i]=dp[i+1]+dp[i+2];
                else
                    dp[i]=dp[i+1];
            }
        }
        return dp[0];
    }
};
```
