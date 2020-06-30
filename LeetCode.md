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

---
给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。
给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。
<div style="text-align:center;vertical-align:middle;">
<img src = 'https://assets.leetcode-cn.com/aliyun-lc-upload/original_images/17_telephone_keypad.png'  width="30%" style="vertical-align: middle"></img>
</div><br>

---
[**解1**]
```java
public List<String> letterCombinations(String digits) {
    List<String> list = new ArrayList<String>();
    // 排除特殊情况
    if(digits == null || digits.length() == 0){
        return list;
    }

    // 建立数字与字母的映射
    Map<Integer, String> map = new HashMap<Integer, String>(){
        {
            put(2, "abc");
            put(3, "def");
            put(4, "ghi");
            put(5, "jkl");
            put(6, "mno");
            put(7, "qprs");
            put(8, "tuv");
            put(9, "wxyz");
        }
    };
    // 开始回溯
    backtrack(digits, new StringBuilder(), list, map);
    return list;
}

public static void backtrack(String moreDigits, StringBuilder combination, List<String> list, Map<Integer, String> map){
    // 终止标志(不再有需要回溯的数字时)
    if(moreDigits.length() == 0){
        list.add(combination.toString());
    }
    else {
        // 取数字
        int digit = moreDigits.charAt(0) - 48;
        // 取字符串
        String letters = map.get(digit);
        for(int i = 0; i < letters.length(); i ++){
            // 取单个字符
            char letter = letters.charAt(i);
            // 进入下一轮(回溯本质)
            backtrack(moreDigits.substring(1), combination.append(letter), list, map);
            // 返回上一轮(删掉进入下一轮时的偏移量)
            combination.deleteCharAt(combination.length() - 1);
        }
    }
}
```
[**解2**]
```java
// 使用二维数组代替map
private static final char[][] dict = new char[][] {
    {'a','b','c'},
    {'d','e','f'},
    {'g','h','i'},
    {'j','k','l'},
    {'m','n','o'},
    {'p','q','r','s'},
    {'t','u','v'},
    {'w','x','y','z'},
};

public List<String> letterCombinations(String digits) {
    List<String> result = new LinkedList<>();
    if (digits.length() > 0) {
        char[] one = new char[digits.length()];
        // 开始回溯
        addChar(digits.toCharArray(), 0, one, result);
    }
    return result;
}

private void addChar(char[] digits, int i, char[] one, List<String> result) {
    // 全部完成
    if (i == digits.length) {
        result.add(new String(one));
        return;
    }
    for (char c : dict[digits[i] - '2']) {
        one[i] = c;
        // 进入下一轮
        addChar(digits, i + 1, one, result);
        // 由于通过数组存值，可以直接覆盖，不用删除偏移量
    }
}
```
[★★★**例2**][LeetCode T46 全排列](https://leetcode-cn.com/problems/permutations/)

---
给定一个没有重复数字的序列，返回其所有可能的全排列。

---
[**解1**]
```java
public static List<List<Integer>> permute(int[] nums) {
    Queue<Integer> queue = new LinkedList<Integer>();
    for(int i : nums){
        queue.offer(i);
    }
    List<List<Integer>> list = new ArrayList<>();
    backtrack(queue, new Stack<>(), list);
    return list;
}

public static void backtrack(Queue<Integer> queue, Stack<Integer> stack, List<List<Integer>> list){
    if(queue.size() == 0){
        list.add(new ArrayList<>(stack));
    }
    else {
        for(int i = 0; i < queue.size(); i ++){
            int ch = queue.poll();
            stack.push(ch);
            backtrack(queue, stack, list);
            stack.pop();
            queue.offer(ch);
        }
    }
}
```
[**解2**]
```java
public List<List<Integer>> permute(int[] nums) {
    int len = nums.length;

    List<List<Integer>> res = new ArrayList<>();
    if (len == 0) {
        return res;
    }

    // 使用位图，适用于数组 nums 的长度不超过 32 位的情况
    int used = 0;
    Stack<Integer> stack = new Stack<>();

    backtrack(nums, 0, len, used, stack, res);
    return res;
}

private void backtrack(int[] nums, int depth, int len, int used, Stack<Integer> stack, List<List<Integer>> res) {
    if (depth == len) {
        res.add(new ArrayList<>(stack));
        return;
    }

    for (int i = 0; i < len; i++) {
        if (((used >> i) & 1) == 0) {
            used ^= (1 << i);
            stack.push(nums[i]);

            backtrack(nums, depth + 1, len, used, stack, res);

            stack.pop();
            used ^= (1 << i);
        }
    }
}
```
[**解3(动态规划)**]
```java
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> dp = new ArrayList<>();
    
    List<Integer> first = new ArrayList<>();
    first.add(nums[0]);
    dp.add(first);
    
    for(int i = 1; i < nums.length; i++) {
        int num = nums[i];
        List<List<Integer>> nextDp = new ArrayList<>();
        for(List<Integer> list : dp) {
            for(int j = 0; j <= list.size(); j++) {
                List<Integer> nList = new ArrayList<>(list);
                nList.add(j, num);
                nextDp.add(nList);
            }
        }
        dp = nextDp;
    }
    return dp;
}
```
[★★★**例3**][LeetCode T47 全排列 II](https://leetcode-cn.com/problems/permutations-ii/)

---
给定一个可包含重复数字的序列，返回所有不重复的全排列。

---
[**解1**]
```java
public List<List<Integer>> permuteUnique(int[] nums) {
    HashSet<List<Integer>> set = new HashSet<>();
    List<List<Integer>> list = new ArrayList<>();
    int len = nums.length, depth = 0, bitmap = 0;
    Arrays.sort(nums);
    if(len == 0){
        return list;
    }
    backtrack(nums, len, bitmap, depth, new Stack<>(), list);
    return list;
}

private void backtrack(int[] nums, int limit, int bitmap, int depth, Stack<Integer> stack, List<List<Integer>> list) {
    if(depth == limit){
        System.out.println(stack);
        list.add(stack);
    }
    else {
        for(int i = 0; i < limit; i ++){
            if(((bitmap >> i) & 1) == 0){
                if(i > 0 && nums[i] == nums[i - 1] && ((bitmap >> (i - 1)) & 1) == 1){
                    continue;
                }
                // not used yet
                bitmap ^= (1 << i);
                stack.push(nums[i]);
                backtrack(nums, limit, bitmap, depth + 1, stack, list);
                stack.pop();
                bitmap ^= (1 << i);
            }
        }
    }
}
```
[★★★**例4**][LeetCode T39 组合总和](https://leetcode-cn.com/problems/permutations-ii/)

---
给定一个无重复元素的数组`candidates`和一个目标数`target`，找出`candidates`中所有可以使数字和为`target`的组合。

`candidates`中的数字可以无限制重复被选取。

---
```java
public List<List<Integer>> combinationSum(int[] candidates, int target) {
    Arrays.sort(candidates);
    List<List<Integer>> list = new ArrayList<>();
    int len = candidates.length;
    if(len == 0){
        return list;
    }
    backtrack(target, len, 0, candidates, new Stack<>(), list);
    return list;
}

public static void backtrack(int diff, int len, int start, int[] candidates, Stack<Integer> stack, List<List<Integer>> list){
    if(diff == 0){
        list.add(new ArrayList<>(stack));
    }
    else {
        // may be founded but not yet
        for(int i = start; i < len && diff - candidates[0] >= 0; i ++){
            stack.push(candidates[i]);
            backtrack(diff - candidates[i], len, i, candidates, stack, list);
            stack.pop();
        }
    }
}
```
