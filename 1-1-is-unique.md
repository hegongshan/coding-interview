#### [面试题 01.01. 判定字符是否唯一](https://leetcode-cn.com/problems/is-unique-lcci/)

实现一个算法，确定一个字符串 s 的所有字符是否全都不同。

**示例 1：**

```
输入: s = "leetcode"
输出: false 
```

**示例 2：**

```
输入: s = "abc"
输出: true
```

**限制：**

* 0 <= len(s) <= 100
* 如果你不使用额外的数据结构，会很加分。

### 方法一：集合

```java
class Solution {
    public boolean isUnique(String astr) {
        Set<Character> set = new HashSet<>();

        for (int i = 0; i < astr.length(); i++) {
            char c = astr.charAt(i);
            if (set.contains(c)) {
                return false;
            }
            set.add(c);
        }
        return true;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为字符串的长度。

### 方法二：哈希表

```java
class Solution {
    public boolean isUnique(String astr) {
        for (int i = 0; i < astr.length(); i++) {
            char c = astr.charAt(i);
            if (astr.indexOf(c) != astr.lastIndexOf(c)) {
                return false;
            }
        }
        return true;
    }
}
```

