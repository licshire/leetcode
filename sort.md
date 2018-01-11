## 排序

---

### 179. Largest Number

###### 描述
Given a list of non negative integers, arrange them such that they form the largest number.

For example, given [3, 30, 34, 5, 9], the largest formed number is 9534330.

Note: The result may be very large, so you need to return a string instead of an integer.

###### 思路
想到把数组按照类似字典序排序，大的在前小的在后，拼接

###### 代码

```
class Solution {
    public String largestNumber(int[] nums) {
        int len = nums.length;
       String[] strs = new String[nums.length];
        
        for (int i = 0; i < len; i++){
            strs[i] = String.valueOf(nums[i]);
        }
        Arrays.sort(strs, new Comparator<String>() {  
            public int compare(String node1, String node2) {
                return (node2+node1).compareTo((node1+node2));
            }  
        });
        String res = "";
        for (int i = 0; i < len; i++){
            if (strs[0].equals("0"))
                return "0";
            res +=  strs[i];
        }
        return res;
    }
}
```
