# 93. Restore IP Addresses - Medium

## Description
Given a string containing only digits, restore it by returning all possible valid IP address combinations.

## Example
```
Input: "25525511135"
Output: ["255.255.11.135", "255.255.111.35"]
```

## Analysis
这道题需要求解一串数字所能分解出的ip地址数目，这种题目类似于求解“子集”问题，采用回溯递归的方式进行求解：先选定一个分割点，再将子集合递归下去进行再分解。

**这里需要注意**：ip地址取值范围0-255，共四位。每一位允许为0，但是不允许XXX.001.XXX这种情况出现

## Solution
```c++
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        vector<string> res;
        string tmp="";
        backtrack(s, 0, 0, res, tmp);
        return res;
    }
    void backtrack(string s, int startIdx, int depth, vector<string>& res, string tmpRes)
    {
        if(depth==4)
        {
            if(startIdx==s.size())
                res.push_back(tmpRes);
            else
                return;
        }
        int sum=0;
        for(int i=0;i<3&&startIdx+i<s.size();i++)
        {
            if(i==0&&s[startIdx]=='0')  // one zero num
            {
                string tmp=s.substr(startIdx,1);
                tmp=tmpRes+tmp;
                if(depth<3)
                    tmp=tmp+".";
                backtrack(s,startIdx+1,depth+1,res,tmp);
                break;
            }
            else
            {
                sum=sum*10+s[i+startIdx]-'0';
                if(sum<256)
                {
                    string tmp=s.substr(startIdx,i+1);
                    tmp=tmpRes+tmp;
                    if(depth<3)
                        tmp=tmp+".";
                    backtrack(s,startIdx+i+1,depth+1,res,tmp);
                }

            }
        }
    }
};
```
