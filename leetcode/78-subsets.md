#### [78. 子集](https://leetcode-cn.com/problems/subsets/)

给定一组**不含重复元素**的整数数组 *nums*，返回该数组所有可能的子集（幂集）。

**说明：**解集不能包含重复的子集。

**示例:**

```java
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

### 回溯

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> list = new LinkedList<>();
        backtrack(0, nums, list, result);
        return result;
    }
    
    private void backtrack(int cur, int[] nums, List<Integer> list, List<List<Integer>> result) {
        if (cur == nums.length) {
            result.add(new ArrayList<>(list));
            return ;
        }
        list.add(nums[cur]);
        backtrack(cur + 1, nums, list, result);
        
        list.remove(list.size() - 1);
        backtrack(cur + 1, nums, list, result);
    }
}
```

