#### [987. 二叉树的垂序遍历](https://leetcode-cn.com/problems/vertical-order-traversal-of-a-binary-tree/)

给定二叉树，按垂序遍历返回其结点值。

对位于 (X, Y) 的每个结点而言，其左右子结点分别位于 (X-1, Y-1) 和 (X+1, Y-1)。

把一条垂线从 X = -infinity 移动到 X = +infinity ，每当该垂线与结点接触时，我们按从上到下的顺序报告结点的值（ Y 坐标递减）。

如果两个结点位置相同，则首先报告的结点值较小。

按 X 坐标顺序返回非空报告的列表。每个报告都有一个结点值列表。

**示例 1：**

<img src="images/binary-tree-example1.png" alt="二叉搜索树1" width="200" height="200">

```
输入：[3,9,20,null,null,15,7]
输出：[[9],[3,15],[20],[7]]
解释： 
在不丧失其普遍性的情况下，我们可以假设根结点位于 (0, 0)：
然后，值为 9 的结点出现在 (-1, -1)；
值为 3 和 15 的两个结点分别出现在 (0, 0) 和 (0, -2)；
值为 20 的结点出现在 (1, -1)；
值为 7 的结点出现在 (2, -2)。
```

**示例 2：**

<img src="images/binary-tree-example2.png" alt="二叉搜索树2" width="300" height="200">

```
输入：[1,2,3,4,5,6,7]
输出：[[4],[2],[1,5,6],[3],[7]]
解释：
根据给定的方案，值为 5 和 6 的两个结点出现在同一位置。
然而，在报告 "[1,5,6]" 中，结点值 5 排在前面，因为 5 小于 6。
```

**提示：**

1. 树的结点数介于 `1` 和 `1000` 之间。
2. 每个结点值介于 `0` 和 `1000` 之间。

### 任意遍历方式+排序

思路：首先，使用任意一种遍历方式，遍历二叉树，与此同时，记录下每个结点的坐标。

然后，对二叉搜索树中的所有结点，按照x坐标升序排列；若x值相同，则按照y坐标降序排列；若y值也相同，则按照结点值升序排列。

最后，按照x值相同与否，加入到不同的列表中。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> verticalTraversal(TreeNode root) {
        List<Point> list = new ArrayList<>();
        preorder(root, 0, 0, list);
        list.sort((a, b) -> {
            if (a.x != b.x) {
                return a.x - b.x;
            }
            if (a.y != b.y) {
                return b.y - a.y;
            }
            return a.val - b.val;
        });

        List<List<Integer>> result = new ArrayList<>();
        result.add(new ArrayList<>());
        // for (int i = 0; i < list.size(); i ++) {
        //     Point p = list.get(i);
        //     result.get(result.size() - 1).add(p.val);
        //     if (i + 1 < list.size() && p.x != list.get(i + 1).x) {
        //         result.add(new ArrayList<>());
        //     }
        // }
      
        Point pre = list.get(0);
        for (Point cur : list) {
            if (pre.x != cur.x) {
                pre = cur;
                result.add(new ArrayList<>());
            }
            result.get(result.size() - 1).add(cur.val);
        }
        return result;
    }

    private void preorder(TreeNode root, int x, int y, List<Point> list) {
        if (root == null) {
            return ;
        }
        list.add(new Point(x, y, root.val));
        preorder(root.left, x - 1, y - 1, list);
        preorder(root.right, x + 1, y - 1, list);
    }

    static class Point {
        int x, y;
        int val;
        Point(int x, int y, int val) {
            this.x = x;
            this.y = y;
            this.val = val;
        }
    }
}
```

复杂度分析：时间复杂度为O(n log n)，空间复杂度为O(n)。其中，n为二叉树中结点的个数。