#### [405. 数字转换为十六进制数](https://leetcode-cn.com/problems/convert-a-number-to-hexadecimal/)

给定一个整数，编写一个算法将这个数转换为十六进制数。对于负整数，我们通常使用 补码运算 方法。

**注意:**

1. 十六进制中所有字母(a-f)都必须是小写。
2. 十六进制字符串中不能包含多余的前导零。如果要转化的数为0，那么以单个字符'0'来表示；对于其他情况，十六进制字符串中的第一个字符将不会是0字符。 
3. 给定的数确保在32位有符号整数范围内。
4. 不能使用任何由库提供的将数字直接转换或格式化为十六进制的方法。

**示例 1：**

```
输入:
26

输出:
"1a"
```

**示例 2：**

```
输入:
-1

输出:
"ffffffff"
```

注意：负整数采用补码形式存储。

```java
class Solution {
    public String toHex(int num) {
        if (num == 0) {
            return "0";
        }
        char[] tableForHex = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'};
        StringBuilder sb = new StringBuilder();
        while (num != 0) {
            sb.append(tableForHex[num & 0b1111]);
            num >>>= 4;
        }
        return sb.reverse().toString();
    }
}
```

