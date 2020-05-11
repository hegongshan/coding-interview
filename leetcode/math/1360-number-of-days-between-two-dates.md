#### [1360. 日期之间隔几天](https://leetcode-cn.com/problems/number-of-days-between-two-dates/)

请你编写一个程序来计算两个日期之间隔了多少天。

日期以字符串形式给出，格式为 `YYYY-MM-DD`，如示例所示。

**示例 1：**

```
输入：date1 = "2019-06-29", date2 = "2019-06-30"
输出：1
```

**示例 2：**

```
输入：date1 = "2020-01-15", date2 = "2019-12-31"
输出：15
```

**提示：**

- 给定的日期是 `1971` 年到 `2100` 年之间的有效日期。

### 方法一：直接计算间隔

```java
class Solution {
    public int daysBetweenDates(String date1, String date2) {

        // 确保date1 < date2
        if (date1.compareTo(date2) > 0) {
            String temp = date1;
            date1 = date2;
            date2 = temp;
        }

        String[] sArr1 = date1.split("-");
        String[] sArr2 = date2.split("-");

        int y1 = Integer.parseInt(sArr1[0]);
        int m1 = Integer.parseInt(sArr1[1]);
        int d1 = Integer.parseInt(sArr1[2]);

        int y2 = Integer.parseInt(sArr2[0]);
        int m2 = Integer.parseInt(sArr2[1]);
        int d2 = Integer.parseInt(sArr2[2]);

        int[][] months = {
          {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31},
          {0, 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31}};
        int day = 0;
        while (y1 < y2 || m1 < m2 || d1 < d2) {
            d1 ++;
            if (d1 == months[isLeapYear(y1) ? 1 : 0][m1] + 1) {
                m1 ++;
                d1 = 1;
            }
            if (m1 == 13) {
                y1 ++;
                m1 = 1;
            }
            day ++;
        }
        return day;
    }

    public int dayOf(int day, int month, int year) {
        int[] months = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

        // 年
        int d = 0;
        for (int y = 1971; y < year; y++) {
            d += 365;
            if (isLeapYear(y)) {
                d += 1;
            }
        }

        // 月
        if (isLeapYear(year)) {
            months[2] += 1;
        }
        for (int m = 1; m < month; m++) {
            d += months[m];
        }

        // 日
        return d + day;
    }

    private boolean isLeapYear(int year) {
        return year % 400 == 0 || (year % 4 == 0 && year % 100 != 0);
    }
}
```

### 方法二：将日期转化为天数

**思路：**将两个日期分别转化为距离1971年1月1日的天数，然后再相减，并对结果取绝对值（date1可能大于date2）。

```java
class Solution {
    public int daysBetweenDates(String date1, String date2) {

        String[] sArr1 = date1.split("-");
        String[] sArr2 = date2.split("-");

        int y1 = Integer.parseInt(sArr1[0]);
        int m1 = Integer.parseInt(sArr1[1]);
        int d1 = Integer.parseInt(sArr1[2]);

        int y2 = Integer.parseInt(sArr2[0]);
        int m2 = Integer.parseInt(sArr2[1]);
        int d2 = Integer.parseInt(sArr2[2]);
      
        return Math.abs(dayOf(d1, m1, y1) - dayOf(d2, m2, y2));
    }

    public int dayOf(int day, int month, int year) {
        int[] months = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

        // 年
        int d = 0;
        for (int y = 1971; y < year; y++) {
            d += 365;
            if (isLeapYear(y)) {
                d += 1;
            }
        }

        // 月
        if (isLeapYear(year)) {
            months[2] += 1;
        }
        for (int m = 1; m < month; m++) {
            d += months[m];
        }

        // 日
        return d + day;
    }

    private boolean isLeapYear(int year) {
        return year % 400 == 0 || (year % 4 == 0 && year % 100 != 0);
    }
}
```



