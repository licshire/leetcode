## 动态规划
#### 一般使用
- 求最大、最小值
- 求方案数
- 求是否可行

#### 类型
- 坐标
- 序列
- 双序列
---

### 单序列

####  132. Palindrome Partitioning II
###### 题目描述：
Given a string s, partition s such that every substring of the partition is a palindrome.
Return the minimum cuts needed for a palindrome partitioning of s.

For example, given s = "aab",
Return 1 since the palindrome partitioning ["aa","b"] could be produced using 1 cut.

###### 思路：
动态规划1"：
- state: f[i]表示前i个字符组成的子串能被分割为最少多少个回文串
- function: f[i] = MIN{f[j]+1}, j < i && j+1 ~ i这一段是一个回文串
- initialize: f[i] = i (f[0] = 0)
- answer: f[n] – 1
动态规划2：
- state: flag[j][i]表示第j 个字符到第i个字符是不是回文
- function: flag[j][i] = true, s[j] == s[i] && flag[j+1][i-1] == true
- initializer: flag[j][i] = false

###### 代码：
```
class Solution {
    
    public int minCut(String s) {
        
        if (s.equals(""))
            return 0;
        
        int[] dp = new int[s.length()];
        boolean[][] flag = new boolean[s.length()][s.length()];
        for (int i = 0; i < s.length(); i++){
            
            int min = i;
            for (int j = 0; j <= i; j++){
                if (s.charAt(j) == s.charAt(i) && (i-j < 2 || flag[j+1][i-1])){
                    flag[j][i] = true;
                    min = j == 0 ? 0 : Math.min(min, dp[j - 1] + 1);
                }
            }
            dp[i] = min;
        }
        return dp[s.length()-1];
    }
}
```
