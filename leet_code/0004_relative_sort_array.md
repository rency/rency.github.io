# [数组相对排序](https://leetcode-cn.com/problems/0H97ZC/)

## 题目描述
给定两个数组，**arr1** 和 **arr2**，
* **arr2** 中的元素各不相同
* **arr2** 中的每个元素都出现在 **arr1** 中  
对 **arr1** 中的元素进行排序，使 **arr1** 中项的相对顺序和 **arr2** 中的相对顺序相同。未在 **arr2** 中出现过的元素需要按照升序放在 **arr1** 的末尾。

### 示例1：
```bash
输入：
arr1 = [2,3,1,3,2,4,6,7,9,2,19],
arr2 = [2,1,4,3,9,6]
输出：
[2,2,2,1,4,3,3,9,6,7,19]
```
### 提示
提示：
* 1 <= arr1.length, arr2.length <= 1000
* 0 <= arr1[i], arr2[i] <= 1000
* arr2 中的元素 arr2[i] 各不相同
* arr2 中的每个元素 arr2[i] 都出现在 arr1 中

## 题解
### 思路
由于题目已提示0 <= arr1[i], arr2[i] <= 1000，要想对 arr1 中的元素按照 arr2 中项的相对顺序进行排序，未在 arr2 中出现过的元素按照升序放在 arr1 的末尾。可以考虑采用***计数排序***来做。
### 步骤
1. 定义一个长度为 1001 的数组 **hash** 。
2. 将 **arr1** 中的所有元素存放在 **hash** 数组中，其中键为 **arr1** 元素，值为 **arr1** 元素出现次数。
3. 定义索引 **index**，初始化为 0，用于重置数组 **arr1** 中的元素值。
4. 遍历数组 **arr2**，只要 **arr2** 中的元素在数组 **hash** 中存在，则将其赋值给 **arr1**，并对该元素在 **hash** 中出现的频次减一；
5. （针对不是 **arr2** 中的元素）遍历整个数组 **hash**，只要其元素出现的次数在一次及以上，将其赋值给 **arr1**，并将该元素在 **hash** 中出现的频次减一。

### 代码
```java
class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        int[] hash = new int[1001];
        for(int n : arr1){
            hash[n] += 1;
        }

        int index = 0;
        for(int n : arr2){
            while(hash[n] > 0){
                arr1[index++] = n;
                hash[n]--;
            }
        }
        for(int i=1; i<hash.length; i++){
            while(hash[i] > 0){
                arr1[index++] = i;
                hash[i]--;
            }
        }
        return arr1;
    }
}
```