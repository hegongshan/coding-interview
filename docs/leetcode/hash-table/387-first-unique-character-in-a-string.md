#### [387. 字符串中的第一个唯一字符](https://leetcode-cn.com/problems/first-unique-character-in-a-string/)

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**案例:**

```
s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
```

**注意事项：**您可以假定该字符串只包含小写字母。

### 方法一：暴力法

```java
class Solution {
    public int firstUniqChar(String s) {
        for (int i = 0; i < s.length(); i++) {
            // 若当前字符不重复
            if (s.indexOf(s.charAt(i)) == s.lastIndexOf(s.charAt(i))) {
                return i;
            }
        }
        return -1;
    }
}
```

复杂度分析：时间复杂度为O($n^2$)，空间复杂度为O(1)。其中，n为字符串的长度。

### 方法二：哈希表

```java
class Solution {
    public int firstUniqChar(String s) {
        Map<Character, Integer> map = new HashMap<>();

        // 值 => 出现次数
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            map.put(c, map.getOrDefault(c, 0) + 1);
        }

        for (int i = 0; i < s.length(); i++) {
            if (map.get(s.charAt(i)) == 1) {
                return i;
            }
        }

        return -1;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为字符串的长度。

### 方法三：用数组实现哈希表

思路：由于给定的字符串只包含小写字母，因此，我们可以使用一个长度为26的数组来表示哈希表。

```java
class Solution {
    public int firstUniqChar(String s) {
        int[] table = new int[26];

        // 值 => 出现次数
        for (int i = 0; i < s.length(); i++) {
            table[s.charAt(i) - 'a'] ++;
        }

        for (int i = 0; i < s.length(); i++) {
            if (table[s.charAt(i) - 'a'] == 1) {
                return i;
            }
        }

        return -1;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(1)。其中，n为字符串的长度。