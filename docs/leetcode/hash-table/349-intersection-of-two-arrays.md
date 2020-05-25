#### [349. 两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

给定两个数组，编写一个函数来计算它们的交集。

**示例 1:**

```
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2]
```

**示例 2:**

```
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [9,4]
```

**说明:**

- 输出结果中的每个元素一定是唯一的。
- 我们可以不考虑输出结果的顺序。

### 方法一：集合

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set1 = new HashSet<>();
        for (int x : nums1) {
            set1.add(x);
        }

        Set<Integer> set2 = new HashSet<>();
        for (int x : nums2) {
            if (set1.contains(x)) {
                set2.add(x);
            }
        }
        return set2.stream().mapToInt(Integer::intValue).toArray();
    }
}
```

复杂度分析：时间复杂度为O(m + n)，空间复杂度为O(m + n)。其中，m和n分别为数组num1和nums2的长度。

### 方法二：retainAll求交集

思路：使用retainAll方法求集合交集。

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set1 = new HashSet<>();
        for (int x : nums1) {
            set1.add(x);
        }

        Set<Integer> set2 = new HashSet<>();
        for (int x : nums2) {
            set2.add(x);
        }
        set1.retainAll(set2);
        return set1.stream().mapToInt(Integer::intValue).toArray();
    }
}
```

复杂度分析：时间复杂度为O(m + n)，空间复杂度为O(m + n)。其中，m和n分别为数组num1和nums2的长度。