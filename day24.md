# 代码随想录算法训练营第二十四天| 77. 组合
作者：Zhiwei Song 
日期：2023-06-16

## 77. 组合
题目链接：[https://leetcode.com/problems/combinations/](https://leetcode.com/problems/combinations/)

思路：学会backtracking的模版以及剪枝的操作。需要二刷。

答案：

```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        backtracking(n, k, res, cur, 0);
        return res;
    }

    private void backtracking(int n, int k, List<List<Integer>> res, List<Integer> cur, int num) {
        if (k == 0) {
            res.add(List.copyOf(cur));
            return;
        }
        for (int i = num; i < n - k + 1; i++) {
            cur.add(i + 1);
            backtracking(n, k - 1, res, cur, i + 1);
            cur.remove(cur.get(cur.size() - 1));
        }
        return;
    }
}
```

时间复杂度：``O(n!)``, 空间复杂度：``O(n!)``
