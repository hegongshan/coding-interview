#### [653. 两数之和 IV - 输入 BST](https://leetcode-cn.com/problems/two-sum-iv-input-is-a-bst/)

给定一个二叉搜索树和一个目标结果，如果 BST 中存在两个元素且它们的和等于给定的目标结果，则返回 true。

**案例 1:**

```
输入: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 9

输出: True
```

**案例 2:**

```
输入: 
    5
   / \
  3   6
 / \   \
2   4   7

Target = 28

输出: False
```

### 方法一：中序遍历+集合

思路：对BST进行中序遍历，遍历的同时将所有的值加入到集合中。然后，依次判断每个值x，其对应的值k-x是否在集合中。

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
    public boolean findTarget(TreeNode root, int k) {
        Set<Integer> set = new HashSet<>();
        inorder(root, set);

        for (Integer x : set) {
            if (x != k - x && set.contains(k - x)) {
                return true;
            }
        }
        return false;
    }

    private void inorder(TreeNode root, Set<Integer> set) {
        if (root == null) {
            return ;
        }
        inorder(root.left, set);
        set.add(root.val);
        inorder(root.right, set);
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为BST中结点的个数。

### 方法二：先序遍历+集合

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
    public boolean findTarget(TreeNode root, int k) {
        Set<Integer> set = new HashSet<>();
        return find(root, k, set);
    }

  	// 先序遍历
    private boolean find(TreeNode root, int k, Set<Integer> set) {
        if (root == null) {
            return false;
        }
        if (set.contains(k - root.val)) {
            return true;
        }
        set.add(root.val);
        return find(root.left, k, set) || find(root.right, k, set);
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为BST中结点的个数。

### 方法三：中序遍历+双指针

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
    public boolean findTarget(TreeNode root, int k) {
        List<Integer> list = new ArrayList<>();
        inorder(root, list);

        int i = 0;
        int j = list.size() - 1;
        int sum = 0;
        while (i < j) {
            sum = list.get(i) + list.get(j);
            if (sum == k) {
                return true;
            } 
            if (sum > k) {
                j--;
            } else {
                i++;
            }
        }
        return false;
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