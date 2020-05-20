#### [633. 平方数之和](https://leetcode-cn.com/problems/sum-of-square-numbers/)

给定一个非负整数 `c` ，你要判断是否存在两个整数 `a` 和 `b`，使得 a^2 + b^2 = c。

**示例1:**

```
输入: 5
输出: True
解释: 1 * 1 + 2 * 2 = 5
```

**示例2:**

```
输入: 3
输出: False
```

### 方法一：开根号

```java
class Solution {
    public boolean judgeSquareSum(int c) {
        int mid = (int) Math.sqrt(c);
        for (int a = 0; a <= mid; a++) {
            double b = Math.sqrt(c - a * a);
            if (b == (int) b) {
                return true;
            }
        }
        return false;
    }
}
```

复杂度分析：时间复杂度为O(√c)，时间复杂度为O(1)。

### 方法二：双指针

```java
class Solution {
    public boolean judgeSquareSum(int c) {
        int left = 0;
        int right = (int) Math.sqrt(c);

        while (left <= right) {
            int sum = left * left + right * right;
            if (sum == c) {
                return true;
            }
            if (sum < c) {
                left ++;
            } else {
                right --;
            }
        }
        return false;
    }
}
```

复杂度分析：时间复杂度为O(√c)，时间复杂度为O(1)。