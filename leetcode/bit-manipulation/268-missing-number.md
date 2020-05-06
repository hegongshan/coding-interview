#### [268. 缺失数字](https://leetcode-cn.com/problems/missing-number/)

给定一个包含 `0, 1, 2, ..., n` 中 *n* 个数的序列，找出 0 .. *n* 中没有出现在序列中的那个数。

**示例 1:**

```
输入: [3,0,1]
输出: 2
```

**示例 2:**

```
输入: [9,6,4,2,3,5,7,0,1]
输出: 8
```

**说明:**
你的算法应具有线性时间复杂度。你能否仅使用额外常数空间来实现?

### 方法一：排序

```java
class Solution {
    public int missingNumber(int[] nums) {
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            if (i != nums[i]) {
                return i;
            }
        }
        return nums.length;
    }
}
```

复杂度分析：时间复杂度为O(n log n)，空间复杂度为O(1)。

### 方法二：等差数列求和

```java
class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        int expectedSum = (n + 1) * n / 2;
        int sum = 0;
        for (int x : nums) {
            sum += x;
        }
        return expectedSum - sum;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(1)。

### 方法三：异或运算

```java
class Solution {
    public int missingNumber(int[] nums) {
        int val = 0;
        for (int i = 0; i < nums.length; i++) {
            val = val ^ i ^ nums[i];
        }
        return val ^ nums.length;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(1)。