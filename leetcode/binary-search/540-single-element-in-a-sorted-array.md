#### [540. 有序数组中的单一元素](https://leetcode-cn.com/problems/single-element-in-a-sorted-array/)

给定一个只包含整数的有序数组，每个元素都会出现两次，唯有一个数只会出现一次，找出这个数。

**示例 1:**

```
输入: [1,1,2,3,3,4,4,8,8]
输出: 2
```

**示例 2:**

```
输入: [3,3,7,7,10,11,11]
输出: 10
```

**注意:** 您的方案应该在 O(log n)时间复杂度和 O(1)空间复杂度中运行。

### 方法一：暴力法

思路：根据题意，数组的长度必为奇数，因此，单一元素e必定出现在奇数位置上。

它的出现会破坏之后的成对状态，即之后的数对x x，第一个x将在偶数位上，第二个x在奇数位上。

如果当前元素nums[i]（i在奇数位）与下一个元素nums[i+1]不相等，则nums[i]就是要找的单一元素；否则，向后移动两位。

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        for (int i = 0; i < nums.length - 1; i += 2) {
            if (nums[i] != nums[i + 1]) {
                return nums[i];
            }
        }
        return nums[nums.length - 1];
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(1)。其中，n为数组的长度。

### 方法二：异或运算

思路：a ^ a = 0；0 ^ a = a。利用这个性质，可以轻松求出单一元素。

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int val = 0;
        for (int x : nums) {
            val ^= x;
        }
        return val;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(1)。其中，n为数组的长度。

### 方法三：二分查找

思路：由于给定数组是有序的，且题目提示我们时间复杂度应该为O(log n)，因此，可以使用二分查找。

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int low = 0;
        int high = nums.length - 1;
        while (low < high) {
            int mid = (low + high) >> 1;
            // 数组的长度为奇数，当low < high时，说明数组中至少有三个元素
            if (nums[mid - 1] != nums[mid] && nums[mid] != nums[mid + 1]) {
                return nums[mid];
            }
            boolean halfIsEven = (mid & 0x1) == 0;
            if (nums[mid - 1] == nums[mid]) {
                if (halfIsEven) {
                    high = mid - 2;
                } else {
                    low = mid + 1;
                }
            } else {
                if (halfIsEven) {
                    low = mid + 2;
                } else {
                    high = mid - 1;
                }
            }
        }
        return nums[low];
    }
}
```

复杂度分析：时间复杂度为O(log n)，空间复杂度为O(1)。其中，n为数组的长度。

### 方法四：仅使用偶数索引的二分查找

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int low = 0;
        int high = nums.length - 1;
        while (low < high) {
            int mid = (low + high) >> 1;
            // 确保mid为偶数
            if ((mid & 0x1) == 1) {
                mid --;
            }
            if (nums[mid] == nums[mid + 1]) {
                low = mid + 2;
            } else {
                high = mid;
            }
        }
        return nums[low];
    }
}
```

复杂度分析：时间复杂度为O(log n)，空间复杂度为O(1)。其中，n为数组的长度。