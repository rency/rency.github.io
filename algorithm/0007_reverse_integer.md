# [整数反转](https://leetcode-cn.com/problems/reverse-integer/)

## 题目描述
给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。

假设环境不允许存储 64 位整数（有符号或无符号）

### 示例1
```bash
输入：x = 123
输出：321
```

### 示例2
```bash
输入：x = -123
输出：-321
```

### 示例3
```bash
输入：x = 120
输出：21
```

### 示例4
```bash
输入：x = 0
输出：0
```

## 题解

### 代码
```java
class Solution {
    public int reverse(int x) {
        if(x == 0){
            return x;
        }
        long res = 0;
        while(x != 0){
            res = res * 10 + x % 10;
            x = x / 10;
        }
        if(res < Integer.MIN_VALUE || res > Integer.MAX_VALUE){
            return 0;
        }
        return (int)res;
    }
}
```