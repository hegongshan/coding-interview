#### [200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

**示例 1:**

```
输入:
11110
11010
11000
00000
输出: 1
```

**示例 2:**

```
输入:
11000
11000
00100
00011
输出: 3
解释: 每座岛屿只能由水平和/或竖直方向上相邻的陆地连接而成。
```

### 方法一：深度优先搜索

思路：本题可以看做求无向图中连通分量的数量。

```java
class Solution {
    public int numIslands(char[][] grid) {
        int m, n;
        if (grid == null || (m = grid.length) == 0 || (n = grid[0].length) == 0) {
            return 0;
        }
        int islandNum = 0; 
        boolean[][] visited = new boolean[m][n];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1' && !visited[i][j]) {
                    dfs(i, j, grid, visited);
                    islandNum ++;
                }
            }
        }
        return islandNum;
    }

    private void dfs(int x, int y, char[][] grid, boolean[][] visited) {
        if (x < 0 || x >= grid.length || y < 0 || y >= grid[0].length || visited[x][y] || grid[x][y] == '0') {
            return ;
        }
        visited[x][y] = true;
        dfs(x + 1, y, grid, visited);
        dfs(x - 1, y, grid, visited);
        dfs(x, y + 1, grid, visited);
        dfs(x, y - 1, grid, visited);
    }
}
```

复杂度分析：时间复杂度为O(m × n)，空间复杂度为O(m × n)。其中，m和n分别为网格的行数和列数。

如果允许改变网格，则空间复杂度可降低为O(1)。

```java
class Solution {
    public int numIslands(char[][] grid) {
        int m, n;
        if (grid == null || (m = grid.length) == 0 || (n = grid[0].length) == 0) {
            return 0;
        }
        int islandNum = 0; 

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1') {
                    dfs(i, j, grid);
                    islandNum ++;
                }
            }
        }
        return islandNum;
    }

    private void dfs(int x, int y, char[][] grid) {
        if (x < 0 || x >= grid.length || y < 0 || y >= grid[0].length || grid[x][y] == '0') {
            return ;
        }
        grid[x][y] = '0';
        dfs(x + 1, y, grid);
        dfs(x - 1, y, grid);
        dfs(x, y + 1, grid);
        dfs(x, y - 1, grid);
    }
}
```

