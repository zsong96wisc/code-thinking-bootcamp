# 代码随想录算法训练营第二十八天| 93.复原IP地址 ，78.子集 ，90.子集II
作者：Zhiwei Song 
日期：2023-06-20

## 93.复原IP地址
题目链接：[https://leetcode.com/problems/restore-ip-addresses/](https://leetcode.com/problems/restore-ip-addresses/)

思路：这里karl用了stringbuilder来manipulate string。需要二刷。

答案：

```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        StringBuilder sb = new StringBuilder(s);
        List<String> res = new ArrayList<>();
        backtracking(sb, res, 0, 0);
        return res;
    }

    private void backtracking(StringBuilder s, List<String> res, int start, int points) {
        if (points == 3 && isValid(s.substring(start, s.length()))) {
            res.add(s.toString());
            return;
        }
        for (int i = start; i < s.length(); i++) {
            if (isValid(s.substring(start, i + 1))) {
                s.insert(i + 1, '.');
                backtracking(s, res, i + 2, points + 1);
                s.deleteCharAt(i + 1);
            } else break;
        }
        return;
    }

    private boolean isValid(String part) {
        if (part.length() > 3 || part == "" || Long.parseLong(part) > 255) {
            return false;
        }
        if (part.length() > 1 && part.charAt(0) == '0') {
            return false;
        }
        return true;
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``

## 78.子集
题目链接：[https://leetcode.com/problems/subsets/](https://leetcode.com/problems/subsets/)

思路：回溯思想。

答案：

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        backtracking(nums, res, cur, 0);
        return res;
    }

    private void backtracking(int[] nums, List<List<Integer>> res, List<Integer> cur, int start) {
        res.add(List.copyOf(cur));
        if (start == nums.length) return;
        for (int i = start; i < nums.length; i++) {
            cur.add(nums[i]);
            backtracking(nums, res, cur, i + 1);
            cur.remove(cur.size() - 1);
        }
        return;
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``

## 90.子集II
题目链接：[https://leetcode.com/problems/subsets-ii/](https://leetcode.com/problems/subsets-ii/)

思路：注意去重，需要二刷！

答案：

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        backtracking(nums, res, cur, 0);
        return res;
    }

    private void backtracking(int nums[], List<List<Integer>> res, List<Integer> cur, int start) {
        res.add(new ArrayList<>(cur));
        for (int i = start; i < nums.length; i++) {
            if (i > start && nums[i] == nums[i - 1]) continue;
            cur.add(nums[i]);
            backtracking(nums, res, cur, i + 1);
            cur.remove(cur.size() - 1);
        }
        return;
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``

