### 树
---
108. Convert Sorted Array to Binary Search Tree

###### 题目描述
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.
For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:
```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```
###### 思路：
  从有序数组中心将数组分成两半， 左右两边数目差为0或1，递归生成平衡二叉搜索树左右子树。时间复杂度O(logn)
  
###### 代码：
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
    public TreeNode sortedArrayToBST(int[] nums) {
        return buildBST(0, nums.length-1, nums);
    }
    
    public TreeNode buildBST(int start, int end, int[] nums){
        int mid = (end + start) / 2;
        if (end < start)
            return null;
        TreeNode node = new TreeNode(nums[mid]);
        if (end == start){
            return node;
        }
        node.left = buildBST(start, mid-1, nums);
        node.right = buildBST(mid+1, end, nums);
        
        return node;
        
    }
}
```

---
##### 109. Convert Sorted List to Binary Search Tree

###### 题目描述
Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.
For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

example:
```
Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

###### 思路：
  从有序链表中心将数组分成两半， 左右两边数目差为0或1，递归生成平衡二叉搜索树左右子树。时间复杂度O(nlogn) 空间复杂度O(logn)
  
###### 代码：
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
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
    public TreeNode sortedListToBST(ListNode head) {
        
        ListNode tmp = head;
        int len = 0;
        while (tmp != null){
            tmp = tmp.next;
            len++;            
        }
        
        return buildBST(head, len);
    }
    
    public TreeNode buildBST(ListNode start, int len){
        
        ListNode midNode = start;
        
        if (len == 0)
            return null;
        
        int mid = len / 2;
        while (mid != 0){
            midNode = midNode.next;
            mid--;
        }
        TreeNode node = new TreeNode(midNode.val);
        
        if (len == 1)
            return node;
        
        node.left = buildBST(start, len/2);
        node.right = buildBST(midNode.next, len-len/2-1);
        
        return node;
        
            
    }
}
```
