#### [1004. 最大连续1的个数 III](https://leetcode-cn.com/problems/max-consecutive-ones-iii/)

给定一个由若干 `0` 和 `1` 组成的数组 `A`，我们最多可以将 `K` 个值从 0 变成 1 。

返回仅包含 1 的最长（连续）子数组的长度。

**示例 1：**

```
输入：A = [1,1,1,0,0,0,1,1,1,1,0], K = 2
输出：6
解释： 
[1,1,1,0,0,1,1,1,1,1,1]
粗体数字从 0 翻转到 1，最长的子数组长度为 6。
```

**示例 2：**

```
输入：A = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], K = 3
输出：10
解释：
[0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1]
粗体数字从 0 翻转到 1，最长的子数组长度为 10。
```

**提示：**

1. `1 <= A.length <= 20000`
2. `0 <= K <= A.length`
3. `A[i]` 为 `0` 或 `1` 

```java
class Solution {
    public int longestOnes(int[] A, int K) {
        // 仅包含1的最长子数组的长度
        int max = 0;
        // 滑动窗口左右边界
        int l = 0, r = 0;
        // 窗口中0的个数
        int zeroCount = 0;
        
        while (r < A.length) {
            if (A[r] == 0) {
                zeroCount ++;
            }
            // 将窗口中0的个数控制在K以内
            while (zeroCount > K) {
                if (A[l] == 0) {
                    zeroCount --;
                }
                l ++;
            }
            max = Math.max(max, r - l + 1);
            r++;
        }
        return max;
    }
}
```

