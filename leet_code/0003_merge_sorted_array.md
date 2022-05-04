# [合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

## 题目描述
给你两个按 *非递减顺序* 排列的整数数组 nums1 和 nums2，另有两个整数 m 和 n ，分别表示 nums1 和 nums2 中的元素数目。

请你 合并 nums2 到 nums1 中，使合并后的数组同样按 *非递减顺序* 排列。

注意：最终，合并后数组不应由函数返回，而是存储在数组 nums1 中。为了应对这种情况，nums1 的初始长度为 m + n，其中前 m 个元素表示应合并的元素，后 n 个元素为 0 ，应忽略。nums2 的长度为 n 。

### 示例 1：
```bash
输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]
解释：需要合并 [1,2,3] 和 [2,5,6] 。
合并结果是 [1,2,2,3,5,6] ，其中斜体加粗标注的为 nums1 中的元素。
```

### 示例 2：
```bash
输入：nums1 = [1], m = 1, nums2 = [], n = 0
输出：[1]
解释：需要合并 [1] 和 [] 。
合并结果是 [1] 
```
### 示例3：
```bash
输入：nums1 = [0], m = 0, nums2 = [1], n = 1
输出：[1]
解释：需要合并的数组是 [] 和 [1] 。
合并结果是 [1] 。
注意，因为 m = 0 ，所以 nums1 中没有元素。nums1 中仅存的 0 仅仅是为了确保合并结果可以顺利存放到 nums1 中。
```
### 提示
```bash
nums1.length == m + n
nums2.length == n
0 <= m, n <= 200
1 <= m + n <= 200
-109 <= nums1[i], nums2[j] <= 109
```
## 题解
### 思路
1. 直接合并后排序
2. 逆向双指针
### 步骤
* 原地使用 **nums1** 数组
* 因 **nums1** 后半部分是空的，可以直接覆盖而不会影响结果。因此可以指针设置为从后向前遍历，每次取两者之中的较大者放进 **nums1** 的最后面
### 代码
1. 直接合并后排序
```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        for (int i = 0; i != n; ++i) {
            nums1[m + i] = nums2[i];
        }
        Arrays.sort(nums1);
    }
}
```
2. 
```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        if(nums1.length != m + n){
            return;
        }
        int pa = m-1,pb=n-1;
        int tail = m + n - 1;
        int curr;
        while(pa >= 0 || pb >= 0){
            if(pa < 0){
                curr = nums2[pb--];
            }else if(pb < 0){
                curr = nums1[pa--];
            }else if(nums1[pa] > nums2[pb]){
                curr = nums1[pa--];
            }else{
                curr = nums2[pb--];
            }
            nums1[tail--] = curr;
        }
    }
}
```