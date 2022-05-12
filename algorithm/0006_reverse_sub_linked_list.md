# [反转子链表](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

## 题目描述
给你单链表的头指针 head 和两个整数 left 和 right ，其中 left <= right 。请你反转从位置 left 到位置 right 的链表节点，返回 反转后的链表 。

### 示例1
<img src='https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg'>

```bash
输入：head = [1,2,3,4,5], left = 2, right = 4
输出：[1,4,3,2,5]
```

### 示例2
```bash
输入：head = [5], left = 1, right = 1
输出：[5]
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
    public ListNode reverseBetween(ListNode head, int left, int right) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;

        //获取子链表的前驱节点
        ListNode pre = dummy;
        for(int i=0; i<left-1; i++){
            pre = pre.next;
        }

        //获取子链表的后驱节点
        ListNode end = pre;
        for(int i=0; i< right - left + 1; i++){
            end = end.next;
        }

        ListNode sub = pre.next;        
        ListNode succ = end.next;

        //原链表中带反转的子链表断开
        pre.next = null;
        end.next = null;

        //反转子链表
        ListNode child = reverse(sub);

        //前驱、后驱、子链表连接
        pre.next = child;
        sub.next = succ;
        return dummy.next;
    }

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