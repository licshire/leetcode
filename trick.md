## 技巧与规律

---
#### 89. Gray Code

###### 题目描述
The gray code is a binary numeral system where two successive values differ in only one bit.
Given a non-negative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.
For example, given n = 2, return [0,1,3,2]. Its gray code sequence is:
```
00 - 0
01 - 1
11 - 3
10 - 2
```
Note:
For a given n, a gray code sequence is not uniquely defined.

For example, [0,2,3,1] is also a valid gray code sequence according to the above definition.

For now, the judge is able to judge based on one instance of gray code sequence. Sorry about that.
###### 思路
列举n=0、1、2、 3：
00,01,11,10 -> (000,001,011,010 ) (110,111,101,100).
n 可以由 n-1得到。
###### 代码

```
class Solution {
    public List<Integer> grayCode(int n) {
        
        List<Integer> res = new ArrayList<>();
        
        res.add(0);
        for (int i = 0; i < n; i++){
            for (int j = res.size()-1; j >= 0; j--){
                res.add(res.get(j) | 1<<i);
            }
        }
        return res;
    }
}
```
