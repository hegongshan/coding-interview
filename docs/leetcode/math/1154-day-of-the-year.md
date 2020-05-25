#### [1154. 一年中的第几天](https://leetcode-cn.com/problems/day-of-the-year/)

给你一个按 YYYY-MM-DD 格式表示日期的字符串 date，请你计算并返回该日期是当年的第几天。

通常情况下，我们认为 1 月 1 日是每年的第 1 天，1 月 2 日是每年的第 2 天，依此类推。每个月的天数与现行公元纪年法（格里高利历）一致。

**示例 1：**

```
输入：date = "2019-01-09"
输出：9
```

**示例 2：**

```
输入：date = "2019-02-10"
输出：41
```

**示例 3：**

```
输入：date = "2003-03-01"
输出：60
```

**示例 4：**

```
输入：date = "2004-03-01"
输出：61
```

**提示：**

* date.length == 10
* date[4] == date[7] == '-'，其他的 date[i] 都是数字。
* date 表示的范围从 1900 年 1 月 1 日至 2019 年 12 月 31 日。

**思路：**使用year表示给定的年，month表示给定的月，day表示给定的天。

1. 首先，判断year是否为闰年，闰年2月有29天。
2. 然后，统计从1月到month-1月的总天数，再加上day，即可得到给定日期是当年的第几天。

```java
class Solution {
    public int dayOfYear(String date) {
        int year = Integer.parseInt(date.substring(0, 4));
        int month = Integer.parseInt(date.substring(5, 7));

        int[] months = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
        // 闰年2月有29天
        if (year % 400 == 0 || (year % 4 == 0 && year % 100 != 0)) {
            months[2] += 1;
        }
        int d = 0;
        for (int m = 1; m < month; m++) {
            d += months[m];
        }

        d += Integer.parseInt(date.substring(8));
        return d;
    }
}
```

