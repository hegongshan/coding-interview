#### [1185. 一周中的第几天](https://leetcode-cn.com/problems/day-of-the-week/)

给你一个日期，请你设计一个算法来判断它是对应一周中的哪一天。

输入为三个整数：day、month 和 year，分别表示日、月、年。

您返回的结果必须是这几个值中的一个 {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"}。

**示例 1：**

```
输入：day = 31, month = 8, year = 2019
输出："Saturday"
```

**示例 2：**

```
输入：day = 18, month = 7, year = 1999
输出："Sunday"
```

**示例 3：**

```
输入：day = 15, month = 8, year = 1993
输出："Sunday"
```

**提示：**

- 给出的日期一定是在 `1971` 到 `2100` 年之间的有效日期。

**思路：**1900年1月1日是星期一；1971年1月1日是星期五。

首先，统计从1900年1月1日到year-1年12月31日的总天数；

然后，再加上从1月到month-1月的总天数；

接着，再加上day，即可得出从1900年1月1日到year年month月day天的总天数d；

最后，d % 7即可得到当前日期对应的星期，其中，0对应星期天。

> 如果起始年为1971年，则可以通过 (d % 7 + 4) % 7得到对应的星期。

```java
class Solution {
    public String dayOfTheWeek(int day, int month, int year) {
        // 1900-01-01 星期一
        // 1971-01-01 星期五
        int[] months = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
        String[] weeks = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};

        // 年
        int d = 0;
        for (int y = 1900; y < year; y++) {
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
        d += day;
        return weeks[d % 7];
    }

    private boolean isLeapYear(int year) {
        if (year % 400 == 0 || (year % 4 == 0 && year % 100 != 0)) {
            return true;
        }
        return false;
    }
}
```

