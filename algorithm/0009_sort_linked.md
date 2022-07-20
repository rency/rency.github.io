#[链表排序](https://leetcode.cn/problems/7WHec2/)

## 题目描述
给定链表的头结点 head ，请将其按 升序 排列并返回 排序后的链表 

### 示例1
```bash
输入：head = [4,2,1,3]
输出：[1,2,3,4]
```

### 示例2
```bash
输入：head = [-1,5,3,4,0]
输出：[-1,0,3,4,5]
```

### 示例3
```bash
输入：head = []
输出：[]
```

## 题解
### 步骤
对链表自顶向下归并排序的过程如下。
1. 找到链表的中点，以中点为分界，将链表拆分成两个子链表。寻找链表的中点可以使用快慢指针的做法，快指针每次移动 22 步，慢指针每次移动 11 步，当快指针到达链表末尾时，慢指针指向的链表节点即为链表的中点。
2. 对两个子链表分别排序。
3. 将两个排序后的子链表合并，得到完整的排序后的链表。

上述过程可以通过递归实现。递归的终止条件是链表的节点个数小于或等于 11，即当链表为空或者链表只包含 11 个节点时，不需要对链表进行拆分和排序。

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
    public ListNode sortList(ListNode head){
        return sort(head,null);
    }

    public ListNode sort(ListNode head,ListNode tail) {
        if(head == null){
            return head;
        }
        if(head.next == tail){
            head.next = null;
            return head;
        }

        ListNode slow = head,fast=head;
        while (fast != tail){
            slow = slow.next;
            fast = fast.next;
            if(fast != tail){
                fast = fast.next;
            }
        }
        ListNode mid = slow;
        ListNode l1 = sort(head,mid);
        ListNode l2 = sort(mid,tail);
        return merge(l1,l2);
    }

    private ListNode merge(ListNode l1, ListNode l2){
        ListNode dummy = new ListNode(-1);
        ListNode temp=dummy, temp1 = l1, temp2=l2;
        while(temp1 != null && temp2 != null){
            if(temp1.val > temp2.val){
                temp.next = temp2;
                temp2 = temp2.next;
            }else{
                temp.next = temp1;
                temp1 = temp1.next;
            }
            temp = temp.next;
        }
        if(temp1 != null){
            temp.next = temp1;
        }
        if(temp2 != null){
            temp.next = temp2;
        }
        return dummy.next;
    }
}
```