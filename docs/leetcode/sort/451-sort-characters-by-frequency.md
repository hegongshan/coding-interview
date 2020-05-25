#### [451. 根据字符出现频率排序](https://leetcode-cn.com/problems/sort-characters-by-frequency/)

给定一个字符串，请将字符串里的字符按照出现的频率降序排列。

**示例 1:**

```
输入:
"tree"

输出:
"eert"

解释:
'e'出现两次，'r'和't'都只出现一次。
因此'e'必须出现在'r'和't'之前。此外，"eetr"也是一个有效的答案。
```

**示例 2:**

```
输入:
"cccaaa"

输出:
"cccaaa"

解释:
'c'和'a'都出现三次。此外，"aaaccc"也是有效的答案。
注意"cacaca"是不正确的，因为相同的字母必须放在一起。
```

**示例 3:**

```
输入:
"Aabb"

输出:
"bbAa"

解释:
此外，"bbaA"也是一个有效的答案，但"Aabb"是不正确的。
注意'A'和'a'被认为是两种不同的字符。
```

### 方法一：哈希表

**思路：**首先，统计字符串中每个字符出现的频率，建立`字符->出现频率`映射关系；

然后，将之前得到的映射关系，转变为`出现频率 -> 字符列表`；

最后，对频率进行降序排序，将所有字符拼接在一起。

#### 代码实现1

```java
class Solution {
    public String frequencySort(String s) {
        // 1.字符 -> 出现频率
        Map<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            map.put(c, map.getOrDefault(c, 0) + 1);
        }

        // 2.按照频率不同，放入不同的桶中
        // 出现频率 -> 字符列表
        Map<Integer, List<Character>> buckets = new HashMap<>();
        for (Map.Entry<Character, Integer> e : map.entrySet()) {
            Character c = e.getKey();
            Integer frequency = e.getValue();
            if (buckets.containsKey(frequency)) {
                buckets.get(frequency).add(c);
            } else {
                List<Character> list = new ArrayList<>();
                list.add(c);
                buckets.put(frequency, list);
            }
        }
        
        // 3.拼接
        StringBuilder sb = new StringBuilder();
        for (int i = s.length(); i >= 1; i--) {
            if (!buckets.containsKey(i)) {
                continue;
            }
            for (Character c : buckets.get(i)) {
                for (int j = 0; j < i; j++) {
                    sb.append(c);
                }
            }
        }
        
        return sb.toString();
    }
}
```

#### 代码实现2

```java
class Solution {
    public String frequencySort(String s) {
        // 1.char -> frequency
        Map<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            map.put(c, map.getOrDefault(c, 0) + 1);
        }

        // 2.frequency -> list
        List<Character>[] buckets = new ArrayList[s.length() + 1];
        for (Map.Entry<Character, Integer> e : map.entrySet()) {
            Integer f = e.getValue();
            if (buckets[f] == null) {
                buckets[f] = new ArrayList<>();
            }
            buckets[f].add(e.getKey());
        }

        // 3.拼接
        StringBuilder sb = new StringBuilder();
        for (int i = buckets.length - 1; i >= 0; i--) {
            if (buckets[i] == null) {
                continue;
            }
            for (Character c : buckets[i]) {
                for (int j = 0; j < i; j++) {
                    sb.append(c);
                }
            }
        }
        return sb.toString();    
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(n)。其中，n为字符串s的长度。