#### [51. N皇后](https://leetcode-cn.com/problems/n-queens/)

*n* 皇后问题研究的是如何将 *n* 个皇后放置在 *n*×*n* 的棋盘上，并且使皇后彼此之间不能相互攻击。

![](/images/8-queens.png)

上图为 8 皇后问题的一种解法。

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。

每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

**示例:**

```
输入: 4
输出: [
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
解释: 4 皇后问题存在两个不同的解法。
```

### 回溯

```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();
        List<String> list = new LinkedList<>();

        char[][] board = new char[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(board[i], '.');
        }

        backtracking(n, board, list, result);
        return result;
    }

    private void backtracking(int n, char[][] board, List<String> list, List<List<String>> result) {
        if (list.size() == n) {
            result.add(new ArrayList<>(list));
            return ;
        }
        int row = list.size();
        // 在当前行寻找插入位置
        for (int i = 0; i < n; i++) {
            // 剪枝
            if (!isValid(board, row, i)) {
                continue;
            }

            board[row][i] = 'Q';
            list.add(new String(board[row]));
            
            backtracking(n, board, list, result);

            board[row][i] = '.';
            list.remove(list.size() - 1);
        }
    }

    private boolean isValid(char[][] board, int row, int column) {
        // 1.当前行
        for (int i = 0; i < column; i ++) {
            if (board[row][i] == 'Q') {
                return false;
            }
        }
        // 2.当前列
        for (int i = 0; i < row; i++) {
            if (board[i][column] == 'Q') {
                return false;
            }
        }
        // 3.左斜线
        int i = row - 1, j = column - 1;
        while (i >= 0 && j >= 0) {
            if (board[i][j] == 'Q') {
                return false;
            }
            i --;
            j --;
        }
        // 4.右斜线
        i = row - 1;
        j = column + 1;
        while (i >= 0 && j >= 0 && j < board.length) {
            if (board[i][j] == 'Q') {
                return false;
            }
            i --;
            j ++;
        }
        return true;
    }
}
```

