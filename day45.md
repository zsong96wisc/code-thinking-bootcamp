# 代码随想录算法训练营第四十五天| 139.单词拆分
作者：Zhiwei Song 
日期：2023-07-08

## 139.单词拆分
题目链接：[https://leetcode.com/problems/word-break/](https://leetcode.com/problems/word-break/)

思路：完全背包就是每一个物品都可以放无限次。这个内层是要从后往前遍历。

答案：

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        boolean[] table = new boolean[s.length() + 1];
        table[0] = true;
        for (int i = 1; i < s.length() + 1; i++) {
            for (int j = i - 1; j >= 0; j--) {
                if (wordDict.contains(s.substring(j, i))) {
                    table[i] = true && table[j];
                    if (table[i]) break;
                }
            }
        }
        return table[s.length()];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``
