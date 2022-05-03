# [两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

## 题目表述
给你两个 *非空* 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

### 示例1：
```bash
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```
### 示例2：
```bash
输入：l1 = [0], l2 = [0]
输出：[0]
```
### 示例3：
```bash
输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
```

### 提示
* 每个链表中的节点数在范围 [1, 100] 内
* 0 <= Node.val <= 9
* 题目数据保证列表表示的数字不含前导零

## 题解：
### 代码
```java
class Solution {
    public ListNode addTwoNumbers(ListNode nodeA, ListNode nodeB) {
        ListNode result = new ListNode(-1);
		ListNode l1 = nodeA;
		ListNode l2 = nodeB;
		ListNode head = result;
		int flag = 0;
		while(l1 != null || l2 != null){
			int sum = flag;
			if(l1 != null){
				sum += l1.val;
				l1 = l1.next;
			}
			if(l2 != null){
				sum += l2.val;
				l2 = l2.next;
			}
			if(sum > 9){
				flag = sum / 10; //取商
				sum -= 10;
			}else{
				flag = 0;
			}
			head.next = new ListNode(sum);
			head = head.next;
		}
		if(flag == 1){
			head.next = new ListNode(1);
		}
		return result.next;
    }
}
```