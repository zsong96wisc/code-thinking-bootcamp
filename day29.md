# 代码随想录算法训练营第二十九天| 491.递增子序列 ，46.全排列 ，47.全排列 II
作者：Zhiwei Song 
日期：2023-06-21

## 491.递增子序列
题目链接：[https://leetcode.com/problems/non-decreasing-subsequences/](https://leetcode.com/problems/non-decreasing-subsequences/)

思路：每一层需要用到set来记录前面看到过的元素。需要二刷。

答案：

```java
class Solution {
    public List<List<Integer>> findSubsequences(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        backtracking(nums, res, new ArrayList<Integer>(), 0);
        return res;
    }

    private void backtracking(int[] nums, List<List<Integer>> res, List<Integer> cur, int start) {
        if (cur.size() >= 2 && cur.get(cur.size() - 1) < cur.get(cur.size() - 2)) return;
        if (cur.size() >= 2) res.add(List.copyOf(cur));
        Set<Integer> used = new HashSet<>();
        for (int i = start; i < nums.length; i++) {
            if (i > start && used.contains(nums[i])) continue;
            used.add(nums[i]);
            cur.add(nums[i]);
            backtracking(nums, res, cur, i + 1);
            cur.remove(cur.size() - 1);
        }
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``

## 46.全排列
题目链接：[https://leetcode.com/problems/permutations/](https://leetcode.com/problems/permutations/)

思路：用一个queue来滚动一遍。

答案：

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Deque<Integer> numbers = new LinkedList<>();
        for (int i : nums) {
            numbers.addLast(i);
        }
        backtracking(numbers, res, new ArrayList<Integer>());
        return res;
    }

    private void backtracking(Deque<Integer> numbers, List<List<Integer>> res, List<Integer> cur) {
        if (numbers.size() == 0) res.add(new ArrayList<>(cur));
        for (int i = 0; i < numbers.size(); i++) {
            int n = numbers.removeFirst();
            cur.add(n);
            backtracking(numbers, res, cur);
            numbers.addLast(n);
            cur.remove(cur.size() - 1);
        }
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``

## 47.全排列 II
题目链接：[https://leetcode.com/problems/permutations-ii/](https://leetcode.com/problems/permutations-ii/)

思路：我用了自己的方法来每一层用set来去重，需要二刷！

答案：

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Deque<Integer> numbers = new LinkedList<>();
        for (int i : nums) {
            numbers.addLast(i);
        }
        backtracking(numbers, res, new ArrayList<Integer>());
        return res;
    }

    private void backtracking(Deque<Integer> numbers, List<List<Integer>> res, List<Integer> cur) {
        if (numbers.size() == 0) res.add(new ArrayList<>(cur));
        Set<Integer> used = new HashSet<>();
        for (int i = 0; i < numbers.size(); i++) {
            int n = numbers.removeFirst();
            if (used.contains(n)) {
                numbers.addLast(n);
                continue;
            }
            used.add(n);
            cur.add(n);
            backtracking(numbers, res, cur);
            numbers.addLast(n);
            cur.remove(cur.size() - 1);
        }
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``

