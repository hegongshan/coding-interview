#### [22. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/)

数字 *n* 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 **有效的** 括号组合。

**示例：**

```
输入：n = 3
输出：[
       "((()))",
       "(()())",
       "(())()",
       "()(())",
       "()()()"
     ]
```

注：2020年4月22日，广联达笔试考到了这个题。

### 方法一：回溯

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list = new ArrayList<>();
        backtracking(0, n, "", list);
        return list;
    }

    public void backtracking(int cur, int n, String s, List<String> list) {
        if (cur == 2 * n) {
            if (isValid(s)) {
                list.add(s);
            }
            return ;
        }
        backtracking(cur + 1, n, s + "(", list);
        backtracking(cur + 1, n, s + ")", list);
    }

    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        int idx = 0;
        while (idx < s.length()) {
            char c = s.charAt(idx++);
            if (c == '(') {
                stack.push('(');
            } else if (stack.isEmpty() || (!stack.isEmpty() && stack.peek() != '(')) {
                return false;
            } else {
                stack.pop();
            }
        }
        return stack.isEmpty();
    }
}
```

### 方法二：回溯+剪枝

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list = new ArrayList<>();
        backtracking(n, 0, 0, "", list);
        return list;
    }

    private void backtracking(int n, int open, int close, String s, List<String> list) {
        // 剪枝
        if (open > n || close > n || open < close) {
            return ;
        }
        if (open == close && open == n) {
            list.add(s);
            return ;
        }
        backtracking(n, open + 1, close, s + "(", list);
        backtracking(n, open, close + 1, s + ")", list);
    }
}
```

### 方法三：回溯+剪枝+字符数组

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list = new ArrayList<>();
        char[] cArr = new char[2 * n];
        backtracking(n, 0, 0, cArr, list);
        return list;
    }

    private void backtracking(int n, int open, int close, char[] cArr, List<String> list) {
        // 剪枝
        if (open > n || close > n || open < close) {
            return ;
        }
        if (open == close && open == n) {
            list.add(new String(cArr));
            return ;
        }
        int cur = open + close;
        cArr[cur] = '(';
        backtracking(n, open + 1, close, cArr, list);

        cArr[cur] = ')';
        backtracking(n, open, close + 1, cArr, list);
    }
}
```

