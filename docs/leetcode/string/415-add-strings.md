#### [415. 字符串相加](https://leetcode-cn.com/problems/add-strings/)

给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和。

注意：

1. num1 和num2 的长度都小于 5100.
2. num1 和num2 都只包含数字 0-9.
3. num1 和num2 都不包含任何前导零。
4. 你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式。

### 模拟加法

思路：模拟加法，从后往前逐位相加，并计算当前位置的值val以及其进位carry。

#### 使用StringBuilder

```java
class Solution {
    public String addStrings(String num1, String num2) {
        if ("0".equals(num1)) {
            return num2;
        }
        if ("0".equals(num2)) {
            return num1;
        }

        int m = num1.length();
        int n = num2.length();

        int i = m - 1, j = n - 1;
        int carry = 0, val = 0;

        StringBuilder sb = new StringBuilder(Math.max(m, n) + 1);
        
        while (i >= 0 || j >= 0) {
            int sum = carry;
            if (i >= 0) {
                sum += num1.charAt(i--) - '0';
            }
            if (j >= 0) {
                sum += num2.charAt(j--) - '0';
            }
            
            val = sum % 10;
            carry = sum / 10;
            
            sb.append(val);           
        }
        
        if (carry > 0) {
            sb.append(carry);
        }
        
        return sb.reverse().toString();
    }
}
```

#### 使用char数组

```java
class Solution {
    public String addStrings(String num1, String num2) {
        if ("0".equals(num1)) {
            return num2;
        }
        if ("0".equals(num2)) {
            return num1;
        }

        int m = num1.length();
        int n = num2.length();

        // 可能有进位，因此，长度为Math.max(m, n) + 1
        char[] arr = new char[Math.max(m, n) + 1];
        int i = m - 1, j = n - 1, k = arr.length;
        int carry = 0, val = 0;

        while (i >= 0 || j >= 0 || carry != 0) {
            int sum = carry;
            if (i >= 0) {
                sum += num1.charAt(i--) - '0';
            }
            if (j >= 0) {
                sum += num2.charAt(j--) - '0';
            }
            // 当前位置的值
            val = sum % 10;
            // 进位
            carry = sum / 10;
            
            arr[--k] = (char) (val + '0'); 
            
        }     
        return new String(arr, k, arr.length - k);
    }
}
```

复杂度分析：时间复杂度为O(max(m, n))，空间复杂度为O(max(m, n))。