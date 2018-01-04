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
