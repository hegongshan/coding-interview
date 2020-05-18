#### [230. 二叉搜索树中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)

给定一个二叉搜索树，编写一个函数 kthSmallest 来查找其中第 k 个最小的元素。

**说明：**
你可以假设 k 总是有效的，1 ≤ k ≤ 二叉搜索树元素个数。

**示例 1:**

```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 1
```

**示例 2:**

```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 3
```

**进阶：**
如果二叉搜索树经常被修改（插入/删除操作）并且你需要频繁地查找第 k 小的值，你将如何优化 `kthSmallest` 函数？

### 方法一：递归

思路：对二叉搜索树进行中序遍历，遍历序列的第k个元素即为二叉搜索树中第k个最小的元素。

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
    private int count = 0;
    private int kth = 0;

    public int kthSmallest(TreeNode root, int k) {
        inorder(root, k);
        return kth;
    }
    // 中序遍历
    private void inorder(TreeNode root, int k) {
        if (root == null) {
            return ;
        }
        inorder(root.left, k);
        count++;
        if (count == k) {
            kth = root.val;
            return ;
        }
        inorder(root.right, k);
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为二叉搜索树中结点的个数。

### 方法二：迭代

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
    public int kthSmallest(TreeNode root, int k) {

        Stack<TreeNode> stack = new Stack<>();
        TreeNode node = root;

        int count = 0;
        // 中序遍历
        while (!stack.isEmpty() || node != null) {
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
            node = stack.pop();
            count ++;
            if (count == k) {
                return node.val;
            }
            node = node.right;
        }
        return 0;
    }
}
```

复杂度分析：时间复杂度为O(H+k)，空间复杂度为O(H+k)。其中，H为二叉搜索树的高度。