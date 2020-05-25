#### [501. 二叉搜索树中的众数](https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/)

给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

* 结点左子树中所含结点的值小于等于当前结点的值
* 结点右子树中所含结点的值大于等于当前结点的值
* 左子树和右子树都是二叉搜索树

例如：给定 BST [1,null,2,2],

```java
   1
    \
     2
    /
   2
```

`返回[2]`.

**提示**：如果众数超过1个，不需考虑输出顺序

**进阶：**你可以不使用额外的空间吗？（假设由递归产生的隐式调用栈的开销不被计算在内）

### 方法一：先遍历，再筛选

思路：首先，通过任意一种遍历方式，对BST进行遍历。遍历的同时，将结点的值x加入哈希表中，并统计其出现的次数。

然后，从哈希表中筛选出出现次数最高的元素。

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
    // 为了在lambda表达式中使用，故定义为实例变量
    private int maxCount = 0;

    public int[] findMode(TreeNode root) {
        Map<Integer, Integer> map = new HashMap<>();
        Stack<TreeNode> stack = new Stack<>();
        // 中序遍历
        TreeNode node = root;
        while (!stack.isEmpty() || node != null) {
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
            node = stack.pop();
            // 更新出现次数
            int cnt = map.getOrDefault(node.val, 0) + 1;
            map.put(node.val, cnt);
            maxCount = Math.max(maxCount, cnt);

            node = node.right;
        }

        return map.entrySet()
                .stream()
                .filter(e -> e.getValue() == maxCount)
                .mapToInt(Map.Entry::getKey)
                .toArray();
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为BST中结点的个数。

### 方法二：遍历和筛选同时进行

思路：BST的中序遍历结果是一个升序序列。在遍历的同时，逐一判断前后两个结点的值是否相等，并更新当前节点值x出现的次数cnt以及最大出现次数maxCount。

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
    private int maxCount = 0;
    private int cnt = 0;
    private TreeNode pre = null;

    public int[] findMode(TreeNode root) {
        List<Integer> list = new LinkedList<>();
        inorder(root, list);
        return list.stream()
                    .mapToInt(Integer::intValue)
                    .toArray();
    }

    public void inorder(TreeNode root, List<Integer> list) {
        if (root == null) {
            return ;
        }
        inorder(root.left, list);
        if (pre != null && pre.val == root.val) {
            cnt ++;
        } else {
            cnt = 1;
        }
        if (maxCount < cnt) {
            list.clear();
            list.add(root.val);
            maxCount = cnt;
        } else if (maxCount == cnt) {
            list.add(root.val);
        }
        pre = root;
        inorder(root.right, list);
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为BST中结点的个数。