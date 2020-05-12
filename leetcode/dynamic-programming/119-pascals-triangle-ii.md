#### [119. 杨辉三角 II](https://leetcode-cn.com/problems/pascals-triangle-ii/)

给定一个非负索引 *k*，其中 *k* ≤ 33，返回杨辉三角的第 *k* 行。

![杨辉三角](images/pascal-triangle-animated.gif)

在杨辉三角中，每个数是它左上方和右上方的数的和。

**示例:**

```
输入: 3
输出: [1,3,3,1]
```

**进阶：**

你可以优化你的算法到 *O*(*k*) 空间复杂度吗？

### 方法一：

**思路：**首先，生成杨辉三角的前 *k* 行（k从0开始）；然后，返回杨辉三角的第*k*行。

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<List<Integer>> triangle = new ArrayList<>(rowIndex + 1);
        triangle.add(Arrays.asList(1));

        for (int i = 1; i <= rowIndex; i++) {
            List<Integer> preRow = triangle.get(i - 1);
            List<Integer> curRow = new ArrayList<>(i + 1);

            curRow.add(1);
            for (int j = 1; j < i; j++) {
                curRow.add(preRow.get(j - 1) + preRow.get(j));
            }
            curRow.add(1);
            
            triangle.add(curRow);
        }
        return triangle.get(rowIndex);
    }
}
```

复杂度分析：时间复杂度为O(k^2)，空间复杂度为O(k^2)。

### 方法二：

**思路：**在杨辉三角中，当前行的值只和前一行相关。因此，只需要保存这两行即可。

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        Integer[] preRow = new Integer[rowIndex + 1];
        Integer[] curRow = new Integer[rowIndex + 1];

        Arrays.fill(preRow, 1);
        Arrays.fill(curRow, 1);

        for (int i = 1; i < curRow.length; i++) {
            // 计算当前行
            curRow[0] = 1;
            for (int j = 1; j < i; j++) {
                curRow[j] = preRow[j - 1] + preRow[j];
            }
            curRow[i] = 1;

            // 更新前一行
            for (int j = 0; j <= i; j++) {
                preRow[j] = curRow[j];
            }
        }
        return Arrays.asList(curRow);
    }
}
```

复杂度分析：时间复杂度为O(k^2)，空间复杂度为O(k)。

### 方法三：

思路：方法二使用了两个数组。实际上，每个数只和它的左上方以及右上方的数相关，我们只需要一个数组即可。

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        Integer[] curRow = new Integer[rowIndex + 1];
        Arrays.fill(curRow, 1);

        for (int i = 1; i < curRow.length; i++) {
            // 计算当前行
            curRow[0] = 1;
            // 由于当前数与其左上方的值有关，因此，可以从后往前计算
            for (int j = i - 1; j > 0; j--) {
                curRow[j] += curRow[j - 1];
            }
            curRow[i] = 1;
        }
        return Arrays.asList(curRow);
    }
}
```

复杂度分析：时间复杂度为O(k^2)，空间复杂度为O(k)。