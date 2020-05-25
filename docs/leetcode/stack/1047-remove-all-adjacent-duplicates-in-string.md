#### [1047. 删除字符串中的所有相邻重复项](https://leetcode-cn.com/problems/remove-all-adjacent-duplicates-in-string/)

给出由小写字母组成的字符串 S，**重复项删除操作**会选择两个相邻且相同的字母，并删除它们。

在 S 上反复执行重复项删除操作，直到无法继续删除。

在完成所有重复项删除操作后返回最终的字符串。答案保证唯一。

**示例：**

```
输入："abbaca"
输出："ca"
解释：
例如，在 "abbaca" 中，我们可以删除 "bb" 由于两字母相邻且相同，这是此时唯一可以执行删除操作的重复项。之后我们得到字符串 "aaca"，其中又只有 "aa" 可以执行重复项删除操作，所以最后的字符串为 "ca"。
```

**提示：**

1. `1 <= S.length <= 20000`
2. `S` 仅由小写英文字母组成。

### 栈

#### 使用Stack

```java
class Solution {
    public String removeDuplicates(String S) {
        Stack<Character> stack = new Stack<>();
        for (char c : S.toCharArray()) {
            if (!stack.isEmpty() && stack.peek() == c) {
                stack.pop();
            } else {
                stack.push(c);
            }
        }

        char[] cArr = new char[stack.size()];
        int index = stack.size() - 1;
        while (!stack.isEmpty()) {
            cArr[index--] = stack.pop();
        }

        return new String(cArr);
    }
}
```

#### 使用数组实现栈

```java
class Solution {
    public String removeDuplicates(String S) {
        int top = -1;
        char[] stack = new char[S.length()];

        for (char c : S.toCharArray()) {
            if (top == -1 || stack[top] != c) {
                stack[++top] = c;
            } else {
                top--;
            }
        }
        return new String(stack, 0, top + 1);
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为字符串S的长度。

