#### [1160. 拼写单词](https://leetcode-cn.com/problems/find-words-that-can-be-formed-by-characters/)

给你一份『词汇表』（字符串数组） words 和一张『字母表』（字符串） chars。

假如你可以用 chars 中的『字母』（字符）拼写出 words 中的某个『单词』（字符串），那么我们就认为你掌握了这个单词。

注意：每次拼写（指拼写词汇表中的一个单词）时，chars 中的每个字母都只能用一次。

返回词汇表 words 中你掌握的所有单词的 长度之和。

**示例 1：**

```
输入：words = ["cat","bt","hat","tree"], chars = "atach"
输出：6
解释： 
可以形成字符串 "cat" 和 "hat"，所以答案是 3 + 3 = 6。
```

**示例 2：**

```
输入：words = ["hello","world","leetcode"], chars = "welldonehoneyr"
输出：10
解释：
可以形成字符串 "hello" 和 "world"，所以答案是 5 + 5 = 10。
```

**提示：**

1. 1 <= words.length <= 1000
2. 1 <= words[i].length, chars.length <= 100
3. 所有字符串中都仅包含小写英文字母

### 哈希表

思路：对于每个单词word，如果其中每个字母出现的次数不大于字母表chars中对应字母的出现次数，那么它就能被拼写出来。

```java
class Solution {
    public int countCharacters(String[] words, String chars) {
        int[] map = new int[26];
        for (int i = 0; i < chars.length(); i++) {
            map[chars.charAt(i) - 'a']++;
        }
        
        int count = 0;
        int[] wordMap = new int[26];
        for (String w : words) {
            boolean canSpell = true;
          
            Arrays.fill(wordMap, 0);
            for (int i = 0; i < w.length(); i++) {
                wordMap[w.charAt(i) - 'a']++;
            }

            for (int i = 0; i < map.length; i++) {
                if (wordMap[i] > map[i]) {
                    canSpell = false;
                    break;
                }
            }
          
            if (canSpell) {
                count += w.length();
            }
        }
        return count;
    }
}
```

复杂度分析：时间复杂度为O(n)，空间复杂度为O(1)。其中，n为词汇表words中所有单词的总长度。