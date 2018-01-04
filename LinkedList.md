## 链表

---

#### 206. Reverse Linked List

###### 题目描述：

Reverse a singly linked list.
click to show more hints.

Hint:
A linked list can be reversed either iteratively or recursively. Could you implement both?

###### 思路：
  链表翻转，加头结点不包含信息，遍历链表，依次前向插入。

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
class Solution {
    public ListNode reverseList(ListNode head) {
        
        ListNode root = new ListNode(-1);
        ListNode tmp = null;
        while(head != null){
            tmp = head.next;
            head.next = root.next;
            root.next = head;
            head = tmp;
        }
        
        return root.next;
    }
}
```

---
#### 92. Reverse Linked List II

###### 题目描述：
Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.

Note:
Given m, n satisfy the following condition:
1 ≤ m ≤ n ≤ length of list.

###### 思路：
  记录第m-1个节点，翻转第m-n个，重新合并，考虑特殊情况：m=1

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
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode res = head;
        int m_ = m;

        int len = n-m+1;
        ListNode pre = head;
        while (m != 1){
            pre = head;
            head = head.next;
            m--;
        }
        
        ListNode root = new ListNode(-1);
        ListNode tail = head;
        
        ListNode tmp = null;
        while(len != 0){
            tmp = head.next;
            head.next = root.next;
            root.next = head;
            head = tmp;
            len--;
        }
        
        pre.next = root.next;
        tail.next = tmp;
        if (m_ == 1)
            return root.next;
        return res;
        
        
    }
}
```
