#### [231. 2的幂](https://leetcode-cn.com/problems/power-of-two/)

给定一个整数，编写一个函数来判断它是否是 2 的幂次方。

**示例 1:**

```
输入: 1
输出: true
解释: 2^0 = 1
```

**示例 2:**

```
输入: 16
输出: true
解释: 2^4 = 16
```

**示例 3:**

```
输入: 218
输出: false
```

### 方法一：递归

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n <= 0) {
            return false;
        }
        if (n == 1) {
            return true;
        }
        return n % 2 == 0 && isPowerOfTwo(n / 2);
    }
}
```

复杂度分析：时间复杂度为O(log n)，空间复杂度为O(log n)。

### 方法二：迭代

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        while (n > 1 && n % 2 == 0) {
            n /= 2;
        }
        return n == 1;
    }
}
```

复杂度分析：时间复杂度为O(log n)，空间复杂度为O(1)。

### 方法三：位运算

思路：若整数n的二进制表示中，只有一个1，则n是2的幂次方。

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        return n > 0 && (n & (n - 1)) == 0;
    }
}
```

复杂度分析：时间复杂度为O(1)，空间复杂度为O(1)。