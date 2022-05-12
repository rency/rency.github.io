# [反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

## 题目描述
给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。

### 示例1：
<img src='https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg'>

```bash
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```

### 示例2
```bash
输入：head = [1,2]
输出：[2,1]
```

### 示例3
```bash
输入：head = []
输出：[]
```

## 题解
### 代码
```java
/**
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode current = head,pre=null;
        while (current!=null){
            ListNode next = current.next;
            current.next = pre;
            pre = current;
            current = next;
        }
        return pre;
    }
}
```