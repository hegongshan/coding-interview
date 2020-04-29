#### [面试题 05.06. 整数转换](https://leetcode-cn.com/problems/convert-integer-lcci/)

整数转换。编写一个函数，确定需要改变几个位才能将整数A转成整数B。

**示例1:**

```
输入：A = 29 （或者0b11101）, B = 15（或者0b01111）
输出：2
```

**示例2:**

```
输入：A = 1，B = 2
输出：2
```

**提示:**

1. A，B范围在[-2147483648, 2147483647]之间

### 方法一：逐位比较

思路：在Java中，int型数据占4个字节，共有32位。因此，可以逐位比较A和B是否相等，统计不相等的位数。

```java
class Solution {
    public int convertInteger(int A, int B) {
        int count = 0;
        for (int i = 0; i < 32; i++) {
            if ((A & 0x1) != (B & 0x1)) {
                count ++;
            }
            A >>= 1;
            B >>= 1;
        }
        return count;
    }
}
```

复杂度分析：时间复杂度为O(1)，空间复杂度为O(1)。

### 方法二：异或运算

思路：题目可以转变为求A与B异或的值中1的个数。而n & (n - 1)可以将n最低位的1转变为0。

```java
class Solution {
    public int convertInteger(int A, int B) {
        int n = A ^ B;
        int count = 0;
        while (n != 0) {
            n &= n - 1;
            count ++;
        }
        return count;
    }
}
```

复杂度分析：时间复杂度为O(1)，空间复杂度为O(1)。