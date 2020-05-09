#### [67. 二进制求和](https://leetcode-cn.com/problems/add-binary/)

给你两个二进制字符串，返回它们的和（用二进制表示）。

输入为 **非空** 字符串且只包含数字 `1` 和 `0`。

**示例 1:**

```
输入: a = "11", b = "1"
输出: "100"
```

**示例 2:**

```
输入: a = "1010", b = "1011"
输出: "10101"
```

**提示：**

* 每个字符串仅由字符 '0' 或 '1' 组成。
* 1 <= a.length, b.length <= 10^4
* 字符串如果不是 "0" ，就都不含前导零。

```java
class Solution {
    public String addBinary(String a, String b) {
        int carry = 0, val;
        int i = a.length() - 1, j = b.length() - 1;
        StringBuilder sb = new StringBuilder();

        while (i >= 0 || j >= 0) {
            val = carry;
            if (i >= 0) {
                val += a.charAt(i--) - '0';
            }
            if (j >= 0) {
                val += b.charAt(j--) - '0';
            }
            carry = val >> 1;
            sb.append(val & 0x1);
        }
        if (carry > 0) {
            sb.append(carry);
        }
        return sb.reverse().toString();
    }
}
```

