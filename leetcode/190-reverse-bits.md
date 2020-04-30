#### [190. 颠倒二进制位](https://leetcode-cn.com/problems/reverse-bits/)

颠倒给定的 32 位无符号整数的二进制位。

**示例 1：**

```java
输入: 00000010100101000001111010011100
输出: 00111001011110000010100101000000
解释: 输入的二进制串 00000010100101000001111010011100 表示无符号整数 43261596，
      因此返回 964176192，其二进制表示形式为 00111001011110000010100101000000。
```

**示例 2：**

```
输入：11111111111111111111111111111101
输出：10111111111111111111111111111111
解释：输入的二进制串 11111111111111111111111111111101 表示无符号整数 4294967293，
      因此返回 3221225471 其二进制表示形式为 10101111110010110010011101101001。
```

**提示：**

* 请注意，在某些语言（如 Java）中，没有无符号整数类型。在这种情况下，输入和输出都将被指定为有符号整数类型，并且不应影响您的实现，因为无论整数是有符号的还是无符号的，其内部的二进制表示形式都是相同的。
* 在 Java 中，编译器使用二进制补码记法来表示有符号整数。因此，在上面的 示例 2 中，输入表示有符号整数 -3，输出表示有符号整数 -1073741825。

**进阶:**
如果多次调用这个函数，你将如何优化你的算法？

### 方法一：模拟

思路：首先，将输入的无符号整数转变为二进制形式（以数组存储）；然后，颠倒二进制数组；最后，将二进制数组还原为无符号整数。

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int[] bits = toBinary(n);
        reverse(bits);
        return toInt(bits);
    }

    private int[] toBinary(int n) {
        int[] bits = new int[32];
        for (int i = bits.length - 1; i >= 0; i--) {
            bits[i] = (n & 0x1);
            n >>>= 1;
        }
        return bits;
    }

    private void reverse(int[] bits) {
        int n = bits.length;
        for (int i = 0; i < (n >> 1); i++) {
            int temp = bits[i];
            bits[i] = bits[n - i - 1];
            bits[n - i - 1] = temp;
        }
    }

    private int toInt(int[] bits) {
        int val = 0;
        for (int x : bits) {
            val = (val << 1) + x;
        }
        return val;
    }
}
```

复杂度分析：时间复杂度为O(1)，空间复杂度为O(1)。

### 方法二：位移运算

思路：将输入的无符号整数逐位翻转。

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int val = 0;
        for (int i = 31; i >= 0; i--) {
            // |用于优化加法运算
            val |= (n & 0x1) << i;
            n >>>= 1;
        }
        return val;
    }
}
```

复杂度分析：时间复杂度为O(1)，空间复杂度为O(1)。