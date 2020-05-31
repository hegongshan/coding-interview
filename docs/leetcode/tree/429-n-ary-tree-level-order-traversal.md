#### [429. N叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)

给定一个 N 叉树，返回其节点值的*层序遍历*。 (即从左到右，逐层遍历)。

例如，给定一个 `3叉树` :

<img src="images/narytreeexample.png" alt="3叉树" width="300" height="200"/>

返回其层序遍历:

```
[
     [1],
     [3,2,4],
     [5,6]
]
```

**说明:**

1. 树的深度不会超过 `1000`。
2. 树的节点总数不会超过 `5000`。

### 方法一：迭代

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            // 逐层遍历
            int size = queue.size();
            List<Integer> list = new ArrayList<>(size);
            for (int i = 0; i < size; i++) {
                Node node = queue.poll();
                list.add(node.val);

                // 将当前节点的孩子节点加入队列中
                for (Node item : node.children) {
                    queue.offer(item);
                }
            }
            result.add(list);      
        }
        return result;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为N叉树中节点的个数。

### 方法二：递归

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root != null) {
            dfs(root, 0, result);
        }
        return result;
    }

    private void dfs(Node root, int level, List<List<Integer>> result) {
        // 若当前层尚未初始化
        if (result.size() < level + 1) {
            result.add(new ArrayList<>());
        }
        result.get(level).add(root.val);
        for (Node item : root.children) {
            dfs(item, level + 1, result);
        }
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O($\log_N n$) ~ O(n)。其中，n为N叉树中节点的个数。