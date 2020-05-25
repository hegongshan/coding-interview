#### [46. 全排列](https://leetcode-cn.com/problems/permutations/)

给定一个 **没有重复** 数字的序列，返回其所有可能的全排列。

**示例:**

```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

### 回溯

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> list = new LinkedList<>();
        boolean[] used = new boolean[nums.length];
        backtrack(nums, used, list, result);
        return result;
    }
    
    public void backtrack(int[] nums, boolean[] used, List<Integer> list, List<List<Integer>> result) {
        if (list.size() == nums.length) {
            result.add(new ArrayList<>(list)); 
            return ;
        }
        for (int i = 0; i < nums.length; i++) {
            if (used[i]) {
                continue;
            }
            used[i] = true;
            list.add(nums[i]);
            
            backtrack(nums, used, list, result);
            
            list.remove(list.size() - 1);
            used[i] = false;
        }
    }
}
```

上述方法存在大量的删除操作等。实际上，这部分操作并不是必须的。

* 优化

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> list = new ArrayList<>(nums.length);
        // 先添加好所有的元素，之后只交换元素，而不进行添加和删除操作
        for (int x : nums) {
            list.add(x);
        }
        backtrack(0, nums, list, result);
        return result;
    }
    
    public void backtrack(int cur, int[] nums, List<Integer> list, List<List<Integer>> result) {
        if (cur == nums.length) {
            result.add(new ArrayList(list));
            return ;
        }
        // 前cur个元素已经确定好
        for (int i = cur; i < nums.length; i++) {
            Collections.swap(list, cur, i);
            
            backtrack(cur + 1, nums, list, result);
            
            Collections.swap(list, cur, i);
        }
    }
}
```

