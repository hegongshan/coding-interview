#### [118. 杨辉三角](https://leetcode-cn.com/problems/pascals-triangle/)

给定一个非负整数 numRows，生成杨辉三角的前 numRows 行。

![杨辉三角](images/pascal-triangle-animated.gif)

在杨辉三角中，每个数是它左上方和右上方的数的和。

**示例:**

```
输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

### 动态规划

**思路：**在杨辉三角中，每行的第一个元素和最后一个元素均为1，中间的数是它左上方和右上方的数的和。

令数组dp表示杨辉三角，则有

```java
dp[i][0] = dp[i][i] = 1;
dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
```

代码如下：

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        if (numRows == 0) {
            return Collections.emptyList();
        }

        List<List<Integer>> triangle = new ArrayList<>(numRows);
        triangle.add(Arrays.asList(1));

        for (int i = 1; i < numRows; i++) {
            List<Integer> preRow = triangle.get(i - 1);
            List<Integer> curRow = new ArrayList<>(i + 1);

            curRow.add(1);
            for (int j = 1; j < i; j++) {
                curRow.add(preRow.get(j - 1) + preRow.get(j));
            }
            curRow.add(1);
            
            triangle.add(curRow);
        }
        return triangle;
    }
}
```

复杂度分析：时间复杂度为O(numRows^2)，空间复杂度为O(numRows^2)。