#### [530. 二叉搜索树的最小绝对差](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/)

给你一棵所有节点为非负值的二叉搜索树，请你计算树中任意两节点的差的绝对值的最小值。

**示例：**

```
输入：

   1
    \
     3
    /
   2

输出：
1

解释：
最小绝对差为 1，其中 2 和 1 的差的绝对值为 1（或者 2 和 3）。
```

**提示：**

- 树中至少有 2 个节点。

### 方法一：先遍历，再求最小

思路：计算BST的中序遍历序列中，相邻两个节点的差，并取最小值。

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

    public int getMinimumDifference(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        inorder(root, list);

        int diff = Integer.MAX_VALUE;
        for (int i = 0; i < list.size() - 1; i++) {
            diff = Math.min(diff, list.get(i + 1) - list.get(i));
        }
        return diff;
    }

    private void inorder(TreeNode root, List<Integer> list) {
        if (root == null) {
            return ;
        }
        inorder(root.left, list);
        list.add(root.val);
        inorder(root.right, list);
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为BST中结点的个数。

### 方法二：遍历与求最小同时进行

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

    private TreeNode pre = null;
    private int diff = Integer.MAX_VALUE;

    public int getMinimumDifference(TreeNode root) {
        inorder(root);
        return diff;
    }

    private void inorder(TreeNode root) {
        if (root == null) {
            return ;
        }
        inorder(root.left);
        if (pre != null) {
            diff = Math.min(diff, root.val - pre.val);
        }
        pre = root;
        inorder(root.right);
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为BST中结点的个数。