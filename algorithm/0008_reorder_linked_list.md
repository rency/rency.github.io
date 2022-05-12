# [重排链表](https://leetcode-cn.com/problems/LGjMqU/)

## 题目描述
给定一个单链表 L 的头节点 head ，单链表 L 表示为：

 L0 → L1 → … → Ln-1 → Ln 
请将其重新排列后变为：

L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → …

不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

### 示例1
<img src='https://pic.leetcode-cn.com/1626420311-PkUiGI-image.png'>

```bash
输入: head = [1,2,3,4]
输出: [1,4,2,3]
```

### 示例2
<img src='https://pic.leetcode-cn.com/1626420320-YUiulT-image.png'>

```bash
输入: head = [1,2,3,4,5]
输出: [1,5,2,4,3]
```

## 题解

### 步骤
**寻找链表中点 + 链表逆序 + 合并链表**

注意到目标链表即为将原链表的左半端和反转后的右半端合并后的结果。
这样我们的任务即可划分为三步：
* [寻找链表中间节点]((https://leetcode-cn.com/problems/middle-of-the-linked-list/))
* [反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)
* 合并链表

### 代码
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public void reorderList(ListNode head) {
        ListNode mid = findMiddleNode(head);

        ListNode l1 = head;
        ListNode l2 = mid.next;
        mid.next = null;

        l2 = reverse(l2);

        merge(l1,l2);
    }

    /**
    * 合并链表
    */
    private void merge(ListNode l1, ListNode l2){
        ListNode l1_temp,l2_temp;
        while( l1 != null && l2 != null){
            l1_temp = l1.next;
            l2_temp = l2.next;

            l1.next = l2;
            l2.next = l1_temp;

            l1 = l1_temp;
            l2 = l2_temp;
        }
    }

    /** 
    * 链表中间节点(快、慢指针)
    */
    private ListNode locateMiddleNode(ListNode head){
        ListNode slow=head,fast=head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    /**
    * 反转链表
    */
    private ListNode reverse(ListNode head){
        ListNode curr = head,pre = null;
        while(curr != null){
            ListNode next = curr.next;
            curr.next = pre;
            pre = curr;
            curr = next;
        }
        return pre;
    }
}
```