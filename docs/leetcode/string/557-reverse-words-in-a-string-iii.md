#### [557. 反转字符串中的单词 III](https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/)

给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

**示例 1:**

```
输入: "Let's take LeetCode contest"
输出: "s'teL ekat edoCteeL tsetnoc"
```

**注意：**在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。

### 双指针

思路：从前往后遍历字符串，寻找每个单词的起始位置start和结束位置end，然后反转该单词。

```java
class Solution {
    public String reverseWords(String s) {
        if (s == null || s.length() <= 1) {
            return s;
        }

        int i = 0;
        char[] arr = s.toCharArray();

        while (i < arr.length) {
            // 寻找单词所在的范围
            int start = i;
            while (i < arr.length && arr[i] != ' ') {
                i ++;
            }
            int end = i - 1;

            // 反转单词
            while (start < end) {
                char temp = arr[start];
                arr[start] = arr[end];
                arr[end] = temp;
                start ++;
                end --;
            }

            // 跳过空格
            i ++;
        }
        return new String(arr);
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为字符串的长度。