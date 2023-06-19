# 代码随想录算法训练营第二十七天| 39. 组合总和 ， 17.电话号码的字母组合 ， 131.分割回文串
作者：Zhiwei Song 
日期：2023-06-19

## 39. 组合总和
题目链接：[https://leetcode.com/problems/combination-sum/](https://leetcode.com/problems/combination-sum/)

思路：回溯思想。

答案：

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        Arrays.sort(candidates);
        backtracking(candidates, target, 0, cur, res);
        return res;
    }

    private void backtracking(int[] candidates, int target, int start, List<Integer> cur, List<List<Integer>> res) {
        if (target == 0) {
            res.add(List.copyOf(cur));
            return;
        }
        
        for (int i = start; i < candidates.length; i++) {
            if (candidates[i] > target) break;
            cur.add(candidates[i]);
            backtracking(candidates, target - candidates[i], i, cur, res);
            cur.remove(cur.size() - 1);
        }
        return;
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``

## 40.组合总和II
题目链接：[https://leetcode.com/problems/combination-sum-ii/](https://leetcode.com/problems/combination-sum-ii/)

思路：需要注意去重。如果数列里后一个数和前一个数是一样的，则不用再去一遍。需要二刷！

答案：

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        Arrays.sort(candidates);
        backtracking(candidates, target, 0, cur, res);
        return res;
    }

    private void backtracking(int[] candidates, int target, int start, List<Integer> cur, List<List<Integer>> res) {
        if (target == 0) {
            res.add(List.copyOf(cur));
            return;
        }
        
        for (int i = start; i < candidates.length; i++) {
            if (candidates[i] > target) break;
            if (i > start && candidates[i] == candidates[i - 1]) continue;
            cur.add(candidates[i]);
            backtracking(candidates, target - candidates[i], i + 1, cur, res);
            cur.remove(cur.size() - 1);
        }
        return;
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``

## 131.分割回文串
题目链接：[https://leetcode.com/problems/palindrome-partitioning/](https://leetcode.com/problems/palindrome-partitioning/)

思路：需要掌握一下DP来减少回文字数量的检查。需要二刷！

答案：

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        List<String> cur = new ArrayList<>();
        backtracking(s, 0, res, cur);
        return res;
    }

    private void backtracking(String s, int start, List<List<String>> res, List<String> cur) {
        if (start == s.length()) {
            res.add(new ArrayList<>(cur));
            return;
        }
        for (int i = start + 1; i <= s.length(); i++) {
            if (isPalindrome(s.substring(start, i))) {
                cur.add(s.substring(start, i));
                backtracking(s, i, res, cur);
                cur.remove(cur.size() - 1);
            }
        }
        return;
    }

    private boolean isPalindrome(String s) {
        if (s.length() == 0) return false;
        for (int i = 0; i < s.length() / 2; i++) {
            if (s.charAt(i) != s.charAt(s.length() - 1 - i)) return false;
        }
        return true;
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``

