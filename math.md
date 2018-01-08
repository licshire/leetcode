## 数学

---
### 172. Factorial Trailing Zeroes

###### 题目描述：
Given an integer n, return the number of trailing zeroes in n!.
Note: Your solution should be in logarithmic time complexity.

###### 思路：
得到0，都由2和5得到，如：
- n = 5: 5以内中包含一个2一个5， res = 1
- n = 15: 15以内包括3个5， res = 3;
答案为5的个数

###### 代码：
```
public class Solution {
    public int trailingZeroes(int n) {
        int r = 0;
        while (n > 0) {
            n /= 5;
            r += n;
        }
        return r;
    }
}
```
