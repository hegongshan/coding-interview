#### [389. 找不同](https://leetcode-cn.com/problems/find-the-difference/)

给定两个字符串 ***s*** 和 ***t***，它们只包含小写字母。

字符串 **t** 由字符串 **s** 随机重排，然后在随机位置添加一个字母。

请找出在 ***t*** 中被添加的字母。

**示例:**

```
输入：
s = "abcd"
t = "abcde"

输出：
e

解释：
'e' 是那个被添加的字母。
```

### 方法一：ASCII码差值

```java
class Solution {
    public char findTheDifference(String s, String t) {
        int val = 0;
        for (int i = 0; i < t.length(); i++) {
            val += t.charAt(i);
        }
        for (int i = 0; i < s.length(); i++) {
            val -= s.charAt(i);
        }      
        return (char) val;
    }
}
```

### 方法二：异或运算

1. a ^ a = 0；
2. 0 ^ a = a。

```java
class Solution {
    public char findTheDifference(String s, String t) {
        int val = 0;
        for (int i = 0; i < s.length(); i++) {
            val ^= s.charAt(i) ^ t.charAt(i);
        }
        val ^= t.charAt(t.length() - 1);
        return (char) val;
    }
}
```

