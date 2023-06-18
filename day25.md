# 代码随想录算法训练营第二十五天| 216.组合总和III ， 17.电话号码的字母组合
作者：Zhiwei Song 
日期：2023-06-17

## 216.组合总和III
题目链接：[https://leetcode.com/problems/combination-sum-iii/](https://leetcode.com/problems/combination-sum-iii/)

思路：回溯基本思想。

答案：

```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        backtracking(k, n, 1, res, cur);
        return res;
    }

    private void backtracking(int k, int n, int start, List<List<Integer>> res, List<Integer> cur) {
        if (k == 0 && n == 0) {
            res.add(List.copyOf(cur));
            return;
        } else if (k == 0 || n == 0) return;

        for (int i = start; i < 10 - k + 1; i++) {
            cur.add(i);
            backtracking(k - 1, n - i, i + 1, res, cur);
            cur.remove(cur.size() - 1);
        }
        return;
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``

## 17.电话号码的字母组合 
题目链接：[https://leetcode.com/problems/letter-combinations-of-a-phone-number/](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

思路：需要建一个dict来map数字和字母。

答案：

```java
class Solution {
    List<String> list = new ArrayList<>();
    StringBuilder temp = new StringBuilder();
    public List<String> letterCombinations(String digits) {
        if (digits.length() == 0) return list;
        String[] numString = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        backtracking(digits, 0, numString);
        return list;
    }

    private void backtracking(String digits, int start, String[] numString) {
        if (start == digits.length()) {
            list.add(temp.toString());
            return;
        }

        String str = numString[digits.charAt(start) - '0'];
        for (int i = 0; i < str.length(); i++) {
            temp.append(str.charAt(i));
            backtracking(digits, start + 1, numString);
            temp.deleteCharAt(temp.length() - 1);
        }
        return;
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``
