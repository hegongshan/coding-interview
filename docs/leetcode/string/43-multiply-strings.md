#### [43. 字符串相乘](https://leetcode-cn.com/problems/multiply-strings/)

给定两个以字符串形式表示的非负整数 `num1` 和 `num2`，返回 `num1` 和 `num2` 的乘积，它们的乘积也表示为字符串形式。

**示例 1:**

```
输入: num1 = "2", num2 = "3"
输出: "6"
```

**示例 2:**

```
输入: num1 = "123", num2 = "456"
输出: "56088"
```

**说明：**

1. num1 和 num2 的长度小于110。
2. num1 和 num2 只包含数字 0-9。
3. num1 和 num2 均不以零开头，除非是数字 0 本身。
4. 不能使用任何标准库的大数类型（比如 BigInteger）或直接将输入转换为整数来处理。

### 模拟乘法

思路：num1和num2的乘积，等于num1与num2中每一位数字的乘积之和。

例如，123 × 456 = 123 × 6 + 123 × 50 + 123 × 400 = 738 + 6150 + 49200 = 56088
$$
\qquad 123 \\\\
\underline{\quad \times 456} \\\\
\qquad 738 \\\\
\quad 615 \\\\
492 \\\\
\overline{\quad 56088}
$$

```java
class Solution {
    public String multiply(String num1, String num2) {
        if ("0".equals(num1) || "0".equals(num2)) {
            return "0";
        }
        // 模拟乘法
        String result = "0";
        for (int i = num2.length() - 1; i >= 0; i--) {
            result = add(result, multiply(num1, num2.charAt(i) - '0', num2.length() - i - 1));
        }
        return result;
    }

    // 计算字符串乘以某一位数字的值
    private String multiply(String num1, int digit, int zeroCount) {
        char[] arr =  new char[num1.length() + 1 + zeroCount];
        int k = arr.length;

        // 在末尾补0
        for (int i = 0; i < zeroCount; i++) {
            arr[--k] = '0';
        }

        int val = 0, carry = 0;
        for (int i = num1.length() - 1; i >= 0; i--) {
            carry += (num1.charAt(i) - '0') * digit;
            arr[--k] = (char) (carry % 10 + '0');
            carry /= 10;
        }
        
        if (carry > 0) {
            arr[--k] = (char) (carry + '0');
        }
        return new String(arr, k, arr.length - k);
    }

    private String add(String num1, String num2) {
        if ("0".equals(num1)) {
            return num2;
        }
        if ("0".equals(num2)) {
            return num1;
        }

        int m = num1.length();
        int n = num2.length();

        // 可能有进位，因此，长度为Math.max(m, n) + 1
        char[] arr = new char[Math.max(m, n) + 1];
        int i = m - 1, j = n - 1, k = arr.length;
        int carry = 0, val = 0;

        while (i >= 0 || j >= 0 || carry != 0) {
            int sum = carry;
            if (i >= 0) {
                sum += num1.charAt(i--) - '0';
            }
            if (j >= 0) {
                sum += num2.charAt(j--) - '0';
            }
            // 当前位置的值
            val = sum % 10;
            // 进位
            carry = sum / 10;

            arr[--k] = (char) (val + '0'); 

        }     
        return new String(arr, k, arr.length - k);
    }
}
```

复杂度分析：时间复杂度为O(m × n)，空间复杂度为O(m + n)。其中，m和n分别为num1和num2的长度。

### 优化

```java
class Solution {
    public String multiply(String num1, String num2) {
        if ("0".equals(num1) || "0".equals(num2)) {
            return "0";
        }
        // 放入各自所在的桶中
        int m = num1.length();
        int n = num2.length();
        int[] buckets = new int[m + n];
        for (int i = m - 1; i >= 0; i--) {
            for (int j = n - 1; j >= 0; j--) {
                buckets[i + j + 1] += (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
                // int val = buckets[i + j + 1] + (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
                // buckets[i + j + 1] = val % 10;
                // buckets[i + j] += val / 10;
            }
        }

        // 处理进位
        int carry = 0;
        for (int i = buckets.length - 1; i >= 0; i--) {
            int val = buckets[i] + carry;
            buckets[i] = val % 10;
            carry = val / 10;
        }

        // 去掉前导0
        int k = 0;
        while (k < buckets.length - 1 && buckets[k] == 0) {
            k ++;
        }

        StringBuilder sb = new StringBuilder();
        while (k < buckets.length) {
            sb.append(buckets[k++]);
        }
        return sb.toString();
    }
}
```

复杂度分析：时间复杂度为O(m × n)，空间复杂度为O(m + n)。其中，m和n分别为num1和num2的长度。

