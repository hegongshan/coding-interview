#### [345. 反转字符串中的元音字母](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)

编写一个函数，以字符串作为输入，反转该字符串中的元音字母。

**示例 1:**

```
输入: "hello"
输出: "holle"
```

**示例 2:**

```
输入: "leetcode"
输出: "leotcede"
```

**说明:**

元音字母不包含字母"y"。

### 方法一：栈

思路：通过入栈和出栈操作，可以字符串反转。

```java
class Solution {

    private char[] vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};

    public String reverseVowels(String s) {
        char[] cArr = s.toCharArray();
        Stack<Character> stack = new Stack<>();

        for (char c : cArr) {
            if (isVowel(c)) {
                stack.push(c);
            }
        }

        for (int i = 0; i < cArr.length; i++) {
            if (isVowel(cArr[i])) {
                cArr[i] = stack.pop();
            }
        }
        
        return new String(cArr);
    }

    private boolean isVowel(char c) {
        for (char vowel : vowels) {
            if (vowel == c) {
                return true;
            }
        }
        return false;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为字符串的长度。

### 方法二：双指针

思路：定义首尾双指针。

每次从前往后寻找元音字母，找到以后，再从后往前寻找元音字母。若存在这样的两个元音字母，则交换它们。

```java
class Solution {

    private char[] vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};

    public String reverseVowels(String s) {
        int left = 0;
        int right = s.length() - 1;
        char[] cArr = s.toCharArray();
        
        while (left < right) {
            while (left < right && !isVowel(cArr[left])) {
                left ++;
            }
            while (left < right && !isVowel(cArr[right])) {
                right --;
            }
            if (left < right) {
                swap(cArr, left, right);
                left ++;
                right --;
            }
        }
        return new String(cArr);
    }

    // 是否为元音字母
    private boolean isVowel(char c) {
        for (char vowel : vowels) {
            if (vowel == c) {
                return true;
            }
        }
        return false;
    }

    private void swap(char[] cArr, int i, int j) {
        char temp = cArr[i];
        cArr[i] = cArr[j];
        cArr[j] = temp;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为字符串的长度。