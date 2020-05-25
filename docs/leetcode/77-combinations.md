#### [77. 组合](https://leetcode-cn.com/problems/combinations/)

给定两个整数 *n* 和 *k*，返回 1 ... *n* 中所有可能的 *k* 个数的组合。

**示例:**

```
输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

### 方法一：回溯

```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> list = new LinkedList<>();
        backtracking(1, n, k, list, result);
        return result;
    }

    private void backtracking(int start, int n, int k, List<Integer> list, List<List<Integer>> result) {
        if (list.size() == k) {
            result.add(new ArrayList<>(list));
            return ;
        }
        for (int i = start; i <= n; i++) {
            list.add(i);
            backtracking(i + 1, n, k, list, result);
            list.remove(list.size() - 1);
        }
    }
}
```

### 方法二：回溯+剪枝

方法一每次从[i,n]中挑选一个元素，然后继续调用backtracking方法。

实际上，每当调用backtracking方法时，已经选出了list.size()个元素，还能再选k - list.size()个元素。

若当前调用backtracking方法时，必须把剩下的元素全部选中，才能组合成k个元素，

换句话说，若当前元素x满足`n - x + 1 = k - list.size()`，`x = n - (k - list.size()) + 1`时，

此时，[x + 1, n]无法挑选出k - list.size()个数，不需要再调用backtracking方法。

因此，每次只需要从[i,n - (k - list.size()) + 1]中挑选一个元素即可。

```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> list = new LinkedList<>();
        backtracking(1, n, k, list, result);
        return result;
    }

    private void backtracking(int start, int n, int k, List<Integer> list, List<List<Integer>> result) {
        if (list.size() == k) {
            result.add(new ArrayList<>(list));
            return ;
        }
        // 剪枝
        for (int i = start; i <= n - (k - list.size()) + 1; i++) {
            list.add(i);
            backtracking(i + 1, n, k, list, result);
            list.remove(list.size() - 1);
        }
    }
}
```

