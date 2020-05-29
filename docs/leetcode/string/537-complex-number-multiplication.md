#### [537. 复数乘法](https://leetcode-cn.com/problems/complex-number-multiplication/)

给定两个表示[复数](https://baike.baidu.com/item/复数/254365?fr=aladdin)的字符串。

返回表示它们乘积的字符串。注意，根据定义 $i^2$ = -1 。

**示例 1:**

```
输入: "1+1i", "1+1i"
输出: "0+2i"
解释: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i ，你需要将它转换为 0+2i 的形式。
```

**示例 2:**

```
输入: "1+-1i", "1+-1i"
输出: "0+-2i"
解释: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i ，你需要将它转换为 0+-2i 的形式。
```

**注意:**

1. 输入字符串不包含额外的空格。
2. 输入字符串将以 a+bi 的形式给出，其中整数 a 和 b 的范围均在 [-100, 100] 之间。输出也应当符合这种形式。

### 思路

根据复数乘法，可以得到
$$
(a + bi) \times (c + di) = ac - bd + (ad + bc)i
$$

#### 使用库函数解析

```java
class Solution {
    public String complexNumberMultiply(String a, String b) {

        String[] complexA = a.split("\\+|i");
        String[] complexB = b.split("\\+|i");

        int realA = Integer.parseInt(complexA[0]);
        int imaginaryA = Integer.parseInt(complexA[1]);

        int realB = Integer.parseInt(complexB[0]);
        int imaginaryB = Integer.parseInt(complexB[1]);

        int real = realA * realB - imaginaryA * imaginaryB;
        int imaginary = realA * imaginaryB + realB * imaginaryA;

        StringBuilder sb = new StringBuilder();
        sb.append(real).append('+').append(imaginary).append('i');
        return sb.toString();
    }
}
```

#### 手动解析

```java
class Solution {
    public String complexNumberMultiply(String a, String b) {
        Complex c1 = parseComplexNumber(a);
        Complex c2 = parseComplexNumber(b);

        int real = c1.real * c2.real - c1.imaginary * c2.imaginary;
        int imaginary = c1.real * c2.imaginary + c2.real * c1.imaginary;

        StringBuilder sb = new StringBuilder();
        sb.append(real).append('+').append(imaginary).append('i');
        return sb.toString();
    }

    private Complex parseComplexNumber(String s) {
        char[] cArr = s.toCharArray();
        int real = 0, imaginary = 0;
        int signReal = 0, signImaginary = 0;

        int i = 0;
        // 处理实部的符号位
        if (cArr[i] == '-') {
            i ++;
            signReal = -1;
        } else if (cArr[i] == '+') {
            i ++;
        }

        // 处理复数的实部
        while (i < cArr.length && '0' <= cArr[i] && cArr[i] <= '9') {
            real = real * 10 + (cArr[i++] - '0');
        }
        // 跳过+号
        i ++;

        // 处理虚部的符号位
        if (cArr[i] == '-') {
            signImaginary = -1;
            i ++;
        }

        // 处理复数的虚部
        while (i < cArr.length && '0' <= cArr[i] && cArr[i] <= '9') {
            imaginary = imaginary * 10 + (cArr[i++] - '0');
        }

        // 补上符号位
        if (signReal < 0) {
            real = -real;
        }
        if (signImaginary < 0) {
            imaginary = -imaginary;
        }
        return new Complex(real, imaginary);
    }

    static class Complex {
        int real;
        int imaginary;

        Complex(int real, int imaginary) {
            this.real = real;
            this.imaginary = imaginary;
        }
    }
}
```

