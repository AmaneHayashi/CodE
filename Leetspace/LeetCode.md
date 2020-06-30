# LeetCode / Data Structure

## 1. Ds
### 1. 链表

### 2. 栈与队列

### 3. 

## 2. Algo
### 1. 回溯(*backtrack*)
- 类型：深度优先搜索(*DFS*)的一种
- 本质：构造状态空间树
- 思路：递归/递推+剪枝

[★★★**例1**][LeetCode T17 电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)
>给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。
给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。
---
[★★★**例2**][LeetCode T46 全排列](https://leetcode-cn.com/problems/permutations/)

> 给定一个没有重复数字的序列，返回其所有可能的全排列。
---
[★★★**例3**][LeetCode T47 全排列 II](https://leetcode-cn.com/problems/permutations-ii/)

> 给定一个可包含重复数字的序列，返回所有不重复的全排列。
---
[★★★**例4**][LeetCode T39 组合总和](https://leetcode-cn.com/problems/permutations-ii/)
> 给定一个无重复元素的数组`candidates`和一个目标数`target`，找出`candidates`中所有可以使数字和为`target`的组合。
- `candidates`中的数字可以无限制重复被选取。
---


给你一个近义词表 `synonyms` 和一个句子 `text` ， `synonyms` 表中是一些近义词对 ，你可以将句子 `text` 中每个单词用它的近义词来替换。

请你找出所有用近义词替换后的句子，按 `字典序排序` 后返回。

[示例]

输入：
`synonyms = [["happy","joy"],["sad","sorrow"],["joy","cheerful"]],
text = "I am happy today but was sad yesterday"`

输出：
`["I am cheerful today but was sad yesterday",`

`"I am cheerful today but was sorrow yesterday",`

`"I am happy today but was sad yesterday",`

`"I am happy today but was sorrow yesterday",`

`"I am joy today but was sad yesterday",`

`"I am joy today but was sorrow yesterday"]`

提示：
- `0 <= synonyms.length <= 10`
- `synonyms[i].length == 2`
- `synonyms[0] != synonyms[1]`
- 所有单词仅包含英文字母，且长度最多为 `10`
- `text` 最多包含 `10 `个单词，且单词间用单个空格分隔开。

---
```java
class Solution {
    private void dfs(Map<String, Set<String>> map, String[] col, List<String> result, int index) {
        if (index == col.length) {
            result.add(String.join(" ", col));
            return;
        }
        if (map.containsKey(col[index])) {
            String s = col[index];
            for (String sub: map.get(col[index])) {
                col[index] = sub;
                dfs(map, col, result, index + 1);
            }
            col[index] = s;
        } else {
            dfs(map, col, result, index + 1);
        }
    }
    public List<String> generateSentences(List<List<String>> synonyms, String text) {
        Map<String, Set<String>> map = new HashMap<>();
        
        for (List<String> synonym: synonyms) {
            Set<String> s1 = map.getOrDefault(synonym.get(0), new HashSet<>());
            Set<String> s2 = map.getOrDefault(synonym.get(1), new HashSet<>());
            if (s1 == s2) {
                continue;
            }
            HashSet<String> ret = new HashSet<>();
            ret.addAll(s1);
            ret.addAll(s2);
            ret.add(synonym.get(0));
            ret.add(synonym.get(1));
            
            for (String sub: ret) {
                map.put(sub, ret);
            }
        }

        String[] col = text.split(" ");
        List<String> result = new ArrayList<>();
        dfs(map, col, result, 0);

        Collections.sort(result);
        return result;
    }
}
```