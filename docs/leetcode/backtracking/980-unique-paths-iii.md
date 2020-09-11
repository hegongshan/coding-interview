#### [980. 不同路径 III](https://leetcode-cn.com/problems/unique-paths-iii/)

在二维网格 grid 上，有 4 种类型的方格：

* 1 表示起始方格。且只有一个起始方格。
* 2 表示结束方格，且只有一个结束方格。
* 0 表示我们可以走过的空方格。
* -1 表示我们无法跨越的障碍。
  返回在四个方向（上、下、左、右）上行走时，从起始方格到结束方格的不同路径的数目。

**每一个无障碍方格都要通过一次，但是一条路径中不能重复通过同一个方格。**

**示例 1：**

```
输入：[[1,0,0,0],[0,0,0,0],[0,0,2,-1]]
输出：2
解释：我们有以下两条路径：
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2)
2. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2)
```

**示例 2：**

```
输入：[[1,0,0,0],[0,0,0,0],[0,0,0,2]]
输出：4
解释：我们有以下四条路径： 
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2),(2,3)
2. (0,0),(0,1),(1,1),(1,0),(2,0),(2,1),(2,2),(1,2),(0,2),(0,3),(1,3),(2,3)
3. (0,0),(1,0),(2,0),(2,1),(2,2),(1,2),(1,1),(0,1),(0,2),(0,3),(1,3),(2,3)
4. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2),(2,3)
```

**示例 3：**

```
输入：[[0,1],[2,0]]
输出：0
解释：
没有一条路能完全穿过每一个空的方格一次。
请注意，起始和结束方格可以位于网格中的任意位置。
```

**提示：**

- `1 <= grid.length * grid[0].length <= 20`

```java
class Solution {
    public int uniquePathsIII(int[][] grid) {
        int m = grid.length, n = grid[0].length;

        int startX = 0, startY = 0, endX = 0, endY = 0;
        int stepNum = 1;

        // 寻找起始和结束方格，并统计路径长度
        outer: for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 0) {
                    stepNum ++;
                } else if (grid[i][j] == 1) {
                    startX = i;
                    startY = j;
                } else if (grid[i][j] == 2) {
                    endX = i;
                    endY = j;
                }
            }
        }

        boolean[][] visited = new boolean[m][n];
        return backtracking(grid, startX, startY, endX, endY, stepNum, visited);
    }

    private int backtracking(int[][] grid, int startX, int startY, int endX, int endY, int stepNum, boolean[][] visited) {
        // 剪枝
        if ((startX < 0 || startX >= grid.length) 
            || (startY < 0 || startY >= grid[0].length)
            || grid[startX][startY] == -1 
            || visited[startX][startY]) {
            return 0;
        }

        // 如果已经到达结束方格
        if (startX == endX && startY == endY) {
            return stepNum == 0 ? 1 : 0;
        }

        // dfs + 回溯
        int count = 0;
        visited[startX][startY] = true;
        count += backtracking(grid, startX, startY - 1, endX, endY, stepNum - 1, visited);
        count += backtracking(grid, startX, startY + 1, endX, endY, stepNum - 1, visited);
        count += backtracking(grid, startX - 1, startY, endX, endY, stepNum - 1, visited);
        count += backtracking(grid, startX + 1, startY, endX, endY, stepNum - 1, visited);
        visited[startX][startY] = false;
        return count;
    }
}
```

