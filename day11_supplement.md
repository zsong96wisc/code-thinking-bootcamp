# 代码随想录算法训练营第十一天（额外练习）| 22. Generate Parentheses ， 1047. 删除字符串中的所有相邻重复项 ， 150. 逆波兰表达式求值 
作者：Zhiwei Song 
日期：2023-06-03

## 22. Generate Parentheses

题目链接： [https://leetcode.com/problems/generate-parentheses/](https://leetcode.com/problems/generate-parentheses/)

思路：此题借鉴了https://blog.csdn.net/qq_34609108/article/details/79031165， 需要二刷。思路是tree的 pre-order traverse。时间复杂度参考卡特兰数。需要二刷！

答案：

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        generateanswers(n, n, "", result);
        return result;
    }

    private void generateanswers(int left, int right, String ret, List<String> result) {
        if (left == 0 && right == 0) {
            result.add(ret);
            return;
        }
        if (left > 0) generateanswers(left - 1, right, ret + "(", result);
        if (right > left) generateanswers(left, right - 1, ret + ")", result);
    }
}
```

时间复杂度：``O(4^n/n^0.5)``, 空间复杂度：``O(n)``
