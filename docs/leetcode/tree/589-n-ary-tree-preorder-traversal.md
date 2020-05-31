#### [589. N叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)

给定一个 N 叉树，返回其节点值的*前序遍历*。

例如，给定一个 `3叉树` :

<img src="images/narytreeexample.png" alt="3叉树" width="300" height="200"/>

返回其前序遍历: `[1,3,5,6,2,4]`。

**说明:** 递归法很简单，你可以使用迭代法完成此题吗?

### 方法一：递归

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
    public List<Integer> preorder(Node root) {
        List<Integer> list = new LinkedList<>();
        if (root == null) {
            return list;
        }
        list.add(root.val);
        for (Node child : root.children) {
            list.addAll(preorder(child));
        }
        return list;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为N叉树中节点的个数。

### 方法二：迭代

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
    public List<Integer> preorder(Node root) {
        List<Integer> list = new LinkedList<>();
        if (root == null) {
            return list;
        }

        Stack<Node> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            Node node = stack.pop();
            list.add(node.val);

            // 叶子结点的children是一个空的List
            List<Node> children = node.children;
            for (int i = children.size() - 1; i >= 0; i--) {
                stack.push(children.get(i));
            }
        }
        return list;

    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为N叉树中节点的个数。