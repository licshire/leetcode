## hash table哈希表

---
### 187. Repeated DNA Sequences

###### 描述
All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

For example,
```
Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",

Return:
["AAAAACCCCC", "CCCCCAAAAA"].
```
###### 思路
利用hash table 记录访问过的子串，用 boolean 记录重复状态。 如果用int 则会内存超限。 
思路2：
  A、C、G、T可以分别用00，01，10，11编码共20位，可以不用string做key 而使用<int, boolean>
###### 代码
```
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        
        List<String> res = new ArrayList<>();
        Map<String, Boolean> map = new HashMap<>();
        
        for (int i = 0; i < s.length()-9; i++){
            String key = s.substring(i, i+10);
            // System.out.println(key);
            if (map.containsKey(key) && map.get(key)){
                res.add(key);
                map.put(key, false);
            } else if (map.containsKey(key)){
                map.put(key, false);
            } else{
                map.put(key, true);
            }
        }
        return res;
    }
}
```
