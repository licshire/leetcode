## 分治算法

---
#### 241. Different Ways to Add Parentheses

###### 题目描述
Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are +, - and *.

```
Example 1
Input: "2-1-1".

((2-1)-1) = 0
(2-(1-1)) = 2
Output: [0, 2]


Example 2
Input: "2*3-4*5"

(2*(3-(4*5))) = -34
((2*3)-(4*5)) = -14
((2*(3-4))*5) = -10
(2*((3-4)*5)) = -10
(((2*3)-4)*5) = 10
Output: [-34, -14, -10, -10, 10]
```

###### 分析
分治法，以每个操作符分割，两部分分别算可能值，再两合并， 避免重复计算，dp记录算过的值

###### 代码
```
class Solution {
    
    Map<String, List<Integer>> map = new HashMap<>();
    public List<Integer> diffWaysToCompute(String input) {

        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < input.length(); i++){
            
            char tmp = input.charAt(i);
            if (tmp == '*' || tmp == '-' || tmp == '+'){
                
                String subLeft = input.substring(0, i);
                String subRight = input.substring(i+1, input.length());
                
                List<Integer> left;
                List<Integer> right;
                
                if (map.containsKey(subLeft)){
                    left = map.get(subLeft);
                } else {
                    left = diffWaysToCompute(subLeft);
                    map.put(subLeft, left);
                }
                if (map.containsKey(subRight)){
                    right = map.get(subRight);
                } else {
                    right = diffWaysToCompute(subRight);
                    map.put(subRight, right);
                }
                
                
                for (int k : left){
                    for (int j : right){
                        if (tmp == '*')
                            res.add(k*j);
                        if (tmp == '-')
                            res.add(k-j);
                        if (tmp == '+')
                            res.add(k+j);
                    }
                }
            }
        }
        if (res.size() == 0)
            res.add(Integer.valueOf(input));
        return res;
    }
}

```

---
#### 95. Unique Binary Search Trees II

###### 题目描述
Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.

For example,
Given n = 3, your program should return all 5 unique BST's shown below.
```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```
###### 解析
分治和dp思想，依次选择1-n做根节点，两边分别再求所有可能情况， 最后依次做为根节点的左右子树。
###### 代码
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<TreeNode> generateTrees(int n) {
        
        if (n == 0)
            return new ArrayList<>();
        List<TreeNode>[][] dp = new List[n+2][n+2];
        return generateTrees(1, n, dp);
    }
    
    public List<TreeNode> generateTrees(int start, int end,List<TreeNode>[][] dp) {
        
        if (dp[start][end] != null)
            return dp[start][end];
        List<TreeNode> res = new ArrayList<>();
            
        if (start > end){
            res.add(null);
            return res;
        }
        if (end == start){
            res.add(new TreeNode(end));
            return res;
        }
        
        for (int i = start; i <= end; i++){
           
            List<TreeNode> lefts = generateTrees(start, i-1, dp);
            List<TreeNode> rights = generateTrees(i+1, end, dp);
            
            for (TreeNode l : lefts){
                for (TreeNode r: rights){
                    TreeNode root = new TreeNode(i);
                    root.left = l;
                    root.right = r;
                    res.add(root);
                }
            }
        } 
        dp[start][end] = res;
        
        return res;
    }
    

}
```

