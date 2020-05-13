#### [150. 逆波兰表达式求值](https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/)

根据逆波兰表示法，求表达式的值。

有效的运算符包括 `+`,` -`, `*`, `/ `。每个运算对象可以是整数，也可以是另一个逆波兰表达式。

**说明：**

* 整数除法只保留整数部分。
* 给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。

**示例 1：**

```
输入: ["2", "1", "+", "3", "*"]
输出: 9
解释: ((2 + 1) * 3) = 9
```

**示例 2：**

```
输入: ["4", "13", "5", "/", "+"]
输出: 6
解释: (4 + (13 / 5)) = 6
```

**示例 3：**

```
输入: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
输出: 22
解释: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

### 方法一：栈

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();
        int x, y;
        for (String token : tokens) {
            if ("+".equals(token)) {
                stack.push(stack.pop() + stack.pop());
            } else if ("-".equals(token)) {
                x = stack.pop();
                y = stack.pop();
                stack.push(y - x);
            } else if ("*".equals(token)) {
                stack.push(stack.pop() * stack.pop());
            } else if ("/".equals(token)) {
                x = stack.pop();
                y = stack.pop();
                stack.push(y / x);
            } else {
                stack.push(Integer.parseInt(token));
            }
        }
        return stack.peek();
    }
}
```

使用switch-case优化if-else：

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();
        int x, y;
        for (String token : tokens) {
            switch (token) {
                case "+":
                    stack.push(stack.pop() + stack.pop());
                    break;
                case "-":
                    x = stack.pop();
                    y = stack.pop();
                    stack.push(y - x);
                    break;
                case "*":
                    stack.push(stack.pop() * stack.pop());
                    break;
                case "/":
                    x = stack.pop();
                    y = stack.pop();
                    stack.push(y / x);
                    break;
                default:
                    stack.push(Integer.parseInt(token));
            }
        }
        return stack.peek();
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为逆波兰表达式的长度。

### 方法二：用数组模拟栈

```java
class Solution {
    public int evalRPN(String[] tokens) {
        int peek = 0;
        int[] nums = new int[tokens.length / 2 + 2];
        for (String token : tokens) {
            if ("+".equals(token)) {
                nums[peek - 1] = nums[peek - 1] + nums[peek];
                peek -= 1;
            } else if ("-".equals(token)) {
                nums[peek - 1] = nums[peek - 1] - nums[peek];
                peek -= 1;
            } else if ("*".equals(token)) {
                nums[peek - 1] = nums[peek - 1] * nums[peek];
                peek -= 1;
            } else if ("/".equals(token)) {
                nums[peek - 1] = nums[peek - 1] / nums[peek];
                peek -= 1;
            } else {
                nums[peek + 1] = Integer.parseInt(token);
                peek += 1;
            }
        }
        return nums[peek];
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为逆波兰表达式的长度。