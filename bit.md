## 位操作

---

### 136. Single Number
###### 描述：
Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

###### 思路：
两个相同的数字异或结果为0， 数组里所有数异或，剩下只出现一次的数

###### 代码：
```
class Solution {
    public int singleNumber(int[] nums) {
        
        int res = nums[0];
        for (int i = 1; i < nums.length; i++){
            res ^= nums[i];
        }
        return res;
    }
}
```
### 137. Single Number II
###### 描述：
Given an array of integers, every element appears three times except for one, which appears exactly once. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

###### 思路：
考虑每个元素的为一个32位的二进制数，这样每一位上出现要么为1 ，要么为0。对数组，统计每一位上1 出现的次数count，必定是3N或者3N+1 次。让count对3取模，能够获得到那个只出现1次的元素该位是0还是1。

###### 代码：
```
class Solution {
    public int singleNumber(int[] nums) {
        
        int len = nums.length;
        int res = 0;
        
        for (int i = 0; i < 32; i++){
            
            int count = 0;
            int mask = 1 << i;
            for (int j = 0; j < nums.length; j++){
                if ((nums[j] & mask) != 0)
                    count++;
            }
            if (count % 3 != 0){
                res |= mask;
            }
        }
        return res;
    }
}
```
### 260. Single Number III
###### 描述：
Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

For example:
Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

Note:
The order of the result is not important. So in the above example, [5, 3] is also correct.
Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?
###### 思路：
假设nums中2个不同的数为a和b，通过计算nums的异或运算就能求出a和b的异或值，定为c。那么c的二进制表示中，从右开始数的第一个1即为a和b的二进制形式在该位上肯定是不同的值。
假如a = 0101, b = 0011, 那么a^b=0110, 那么a和b是在从右往左数的第二位值不同。设置bit=010，将nums里的每个数&bit, 便可将nums分成2组了，每组的异或值就是a或者b了。

###### 代码：
```
class Solution {
    public int[] singleNumber(int[] nums) {

        int xo = 0;
        for (int i: nums){
            xo ^= i;
        }
        
        xo &= -xo; // 得到最后一位不同的mask;
        int[] res = {0, 0};
        for (int i: nums){ //分成两组，分别异或
            if ((i & xo) == 0){
                res[0] ^= i;
            } else {
                res[1] ^= i;
            }
        }
        
        return res;
    }
}
```


