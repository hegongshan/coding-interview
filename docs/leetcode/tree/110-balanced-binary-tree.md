#### [110. 平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

> 一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。

**示例 1:**

给定二叉树 `[3,9,20,null,null,15,7]`

```
    3
   / \
  9  20
    /  \
   15   7
```

返回 `true` 。
**示例 2:**

给定二叉树 `[1,2,2,3,3,null,null,4,4]`

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

返回 `false` 。

### 方法一：自顶向下递归

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
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        return Math.abs(height(root.left) - height(root.right)) <= 1 
            && isBalanced(root.left) 
            && isBalanced(root.right);
    }

    // 计算给定结点的高度
    public int height(TreeNode root) {
        if (root == null) {
            return -1;
        }
        return 1 + Math.max(height(root.left), height(root.right));
    }
}
```

复杂度分析：时间复杂度为O(n log n)，空间复杂度为O(n)。其中，n为二叉树中结点的个数。

### 方法二：自底向上递归

思路：方法一在计算高度时，存在大量的重复计算。

实际上，我们可以采用自底向上递归，存储每个结点的高度，从而避免重复计算。

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

    class Info {
        int height;
        boolean balanced;
        Info (int height, boolean balanced) {
            this.height = height;
            this.balanced = balanced;
        }
    }

    public boolean isBalanced(TreeNode root) {
        return isBalanced0(root).balanced;
    }

    public Info isBalanced0(TreeNode root) {
        if (root == null) {
            return new Info(-1, true);
        }

        Info left = isBalanced0(root.left);
        Info right = isBalanced0(root.right);

        int height = 1 + Math.max(left.height, right.height);
        boolean balanced = left.balanced && right.balanced && Math.abs(left.height - right.height) <= 1;
        return new Info(height, balanced);
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为二叉树中结点的个数。