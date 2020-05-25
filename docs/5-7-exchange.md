#### [面试题 05.07. 配对交换](https://leetcode-cn.com/problems/exchange-lcci/)

配对交换。编写程序，交换某个整数的奇数位和偶数位，尽量使用较少的指令（也就是说，位0与位1交换，位2与位3交换，以此类推）。

**示例1:**

```
输入：num = 2（或者0b10）
输出 1 (或者 0b01)
```

**示例2:**

```
输入：num = 3
输出：3
```

**提示:**

1. `num`的范围在[0, 2^30 - 1]之间，不会发生整数溢出。

### 方法一：模拟

思路：首先，将num转变为二进制形式；然后，交换奇数位和偶数位；最后，还原为整数。

```java
class Solution {
    public int exchangeBits(int num) {
        int[] arr = toBinary(num);
        for (int i = 0; i < arr.length; i += 2) {
            int temp = arr[i];
            arr[i] = arr[i + 1];
            arr[i + 1] = temp;
        }
        return toInt(arr);
    }

    private int[] toBinary(int num) {
        int[] arr = new int[32];
        for (int i = arr.length - 1; i >= 0; i--) {
            arr[i] = (num & 0x1);
            num >>>= 1;
        }
        return arr;
    }

    private int toInt(int[] arr) {
        int val = 0;
        for (int i = 0; i < arr.length; i++) {
            val = 2 * val + arr[i];
        }
        return val;
    }
    
}
```

复杂度分析：时间复杂度为O(1)，空间复杂度为O(1)。

### 方法二：

思路：

0x55555555 = 0b 0101 0101 0101 0101 0101 0101 0101 0101

0xaaaaaaaa = 0b 1010 1010 1010 1010 1010 1010 1010 1010

num & 0x55555555可以得到num中的所有偶数位even；num & 0xaaaaaaaa可以得到num中的所有奇数位odd。

交换奇数位和偶数位，等价于让even左移一位，让odd右移一位，然后对even和odd执行或运算。

```java
class Solution {
    public int exchangeBits(int num) {
        // 1.计算奇数位和偶数位的值
        int even = num & 0x55555555;
        int odd = num & 0xaaaaaaaa;

        // 2.交换奇数位和偶数位
        return (even << 1) | (odd >> 1);
        // return ((num & 0x55555555) << 1) | ((num & 0xaaaaaaaa) >> 1);
    }    
}
```

复杂度分析：时间复杂度为O(1)，空间复杂度为O(1)。