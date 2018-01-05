## 回溯

---

#### 77. Combinations

###### 题目描述
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:
```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

###### 思路：

回溯方法，递归实现：终止条件k=0, 

###### 代码：

```
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<Integer> tmp = new ArrayList<>();
        List<List<Integer>> res = new ArrayList<>();
        backtracking(1, n, k, tmp, res);
        return res;
    }
    
    public void backtracking(int start, int n, int k, List<Integer> tmp, List<List<Integer>> res){
        
        if (k == 0){
            res.add(new ArrayList(tmp));
            return;
        }
        
        for (int i = start; i <= n; i++){
            tmp.add(i);
            backtracking(i+1, n, k-1, tmp, res);
            tmp.remove(tmp.size()-1);
            
        }
        
    }
}
```
---

#### 131. Palindrome Partitioning
###### 题目描述：

Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

For example, given s = "aab",
Return
```
[
  ["aa","b"],
  ["a","a","b"]
]
```

###### 思路：
回溯方法，遍历所有可能，当前子串不为回文时跳过递归。
###### 代码：
```
class Solution {
    public List<List<String>> partition(String s) {
        
        List<List<String>> res = new ArrayList<>();
        List<String> tmp = new ArrayList<>();
        solve(0, s, tmp, res);
        
        return res;
    }
    
    public void solve(int start, String s, List<String> tmp, List<List<String>> res){
        int len = s.length();
        
        if (start >= len){
            res.add(new ArrayList(tmp));
            return;
        }
        
        for (int i = start+1; i <= len; i++){ // i 为子字符串end位置。
            String sub = s.substring(start, i);
            if (!checkPalindrome(sub)){
                continue;
            }
            tmp.add(sub);
            solve(i, s, tmp, res);
            tmp.remove(tmp.size()-1);
        }
    }
    
    public boolean checkPalindrome(String sub){
        
        int end = sub.length()-1;
        int start = 0;
        while(start <= end){
            if (sub.charAt(start) != sub.charAt(end)){
                return false;
            }
            start++;
            end--;
        }
        return true;
    }
}
```
