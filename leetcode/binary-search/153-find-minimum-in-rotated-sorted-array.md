#### [153. 寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。

**示例 1:**

```
输入: [3,4,5,1,2]
输出: 1
```

**示例 2:**

```
输入: [4,5,6,7,0,1,2]
输出: 0
```

### 方法一：暴力法

思路：从前往后遍历数组。若存在某一个元素，满足：它的前一个元素大于它自己，则该元素就是要求的最小值。若不存在这样的元素，则表示数组在旋转后仍然是有序的（旋转点为0），此时，第一个元素就是要求的最小值。

```java
class Solution {
    public int findMin(int[] nums) {
        for (int i = 1; i < nums.length; i++) {
            if (nums[i - 1] > nums[i]) {
                return nums[i];
            }
        }
        return nums[0];
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(1)。

### 方法二：二分查找

思路：假设数组的长度为n，旋转之后，数组被分成了两个有序区域[0, x - 1]和[x, n - 1]，它们均按照升序排列，并且[0, x - 1]中的值大于[x, n - 1]中的值。

可以采用二分查找：如果nums[mid] < nums[high]，则表示最小值在[low, mid]中；否则，表示最小值在[mid + 1, high]中。

```java
class Solution {
    public int findMin(int[] nums) {
        int low = 0;
        int high = nums.length - 1;
        while (low < high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] < nums[high]) {
                high = mid;        
            } else {
                low = mid + 1;
            }
        }
        return nums[low];
    }
}
```

复杂度分析：时间复杂度为O(log n)，空间复杂度为O(1)。