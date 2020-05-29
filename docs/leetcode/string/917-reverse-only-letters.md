#### [917. 仅仅反转字母](https://leetcode-cn.com/problems/reverse-only-letters/)

给定一个字符串 `S`，返回 “反转后的” 字符串，其中不是字母的字符都保留在原地，而所有字母的位置发生反转。

**示例 1：**

```
输入："ab-cd"
输出："dc-ba"
```

**示例 2：**

```
输入："a-bC-dEf-ghIj"
输出："j-Ih-gfE-dCba"
```

**示例 3：**

```
输入："Test1ng-Leet=code-Q!"
输出："Qedo1ct-eeLg=ntse-T!"
```

**提示：**

1. `S.length <= 100`
2. `33 <= S[i].ASCIIcode <= 122` 
3. `S` 中不包含 `\` or `"`

### 双指针

思路：首先，从前往后遍历字符串，寻找遇到的第一个字母。然后，从后往前遍历字符串，寻找遇到的第一个字母。如果存在这样的两个字母，则交换它们。

```java
class Solution {
    public String reverseOnlyLetters(String S) {
        int i = 0;
        int j = S.length() - 1;

        char[] arr = S.toCharArray();
        while (i < j) {
            while (i < j && !isLetter(arr[i])) {
                i ++;
            }
            while (i < j && !isLetter(arr[j])) {
                j --;
            }
            if (i < j) {
                char temp = arr[i];
                arr[i] = arr[j];
                arr[j] =temp;
                i ++;
                j --;
            }
        }
        return new String(arr);
    }

    private boolean isLetter(char c) {
        return ('a' <= c && c <= 'z') || ('A' <= c && c <= 'Z');
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为字符串的长度。