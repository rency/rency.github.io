# [两数之和](https://leetcode-cn.com/problems/two-sum/)

## 题目描述
给定一个整数数组 **nums** 和一个整数目标值 **target**，请你在该数组中找出 两数之和为目标值 **target**  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。
### 示例1
```bash
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```
### 示例2
```bash
输入：nums = [3,2,4], target = 6
输出：[1,2]
```
### 示例3
```bash
输入：nums = [3,3], target = 6
输出：[0,1]
```
### 提示
* 2 <= nums.length <= 104
* -109 <= nums[i] <= 109
* -109 <= target <= 109
* 只会存在一个有效答案

## 题解
### 思路
> 哈希表  
使用哈希表，可以将寻找 target - x 的时间复杂度降低到从 O(N)O(N) 降低到 O(1)O(1)。  
这样我们创建一个哈希表，对于每一个 x，我们首先查询哈希表中是否存在 target - x，然后将 x 插入到哈希表中，即可保证不会让 x 和自己匹配。

### 代码
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer,Integer> map = new HashMap<>();
        for(int i=0; i< nums.length; i++){
            int diff = target - nums[i];
            if(map.get(diff) != null){
                return new int[]{map.get(diff),i};
            }
            map.put(nums[i],i);
        }
        return new int[]{-1,-1};
    }
}
```