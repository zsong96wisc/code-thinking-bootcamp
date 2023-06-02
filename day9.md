# 代码随想录算法训练营第九天| 28. 实现 strStr() ，459.重复的子字符串
作者：Zhiwei Song 
日期：2023-06-01

## 28. 实现 strStr()
题目链接： [https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/]([https://leetcode.com/problems/4sum-ii/](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/))

思路：KMP, KMP, 需要画图，需要二刷！！！难！

答案：

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.length() == 0) return 0;
        int[] next = new int[needle.length()];
        getNext(next, needle);

        int j = 0;
        for (int i = 0; i < haystack.length(); i++) {
            while (j > 0 && needle.charAt(j) != haystack.charAt(i)) 
                j = next[j - 1];
            if (needle.charAt(j) == haystack.charAt(i)) j++;
            if (j == needle.length()) return i - needle.length() + 1;
        }
        return -1;
    }
    
    private void getNext(int[] next, String s) {
        int j = 0;
        next[0] = 0;
        for (int i = 1; i < s.length(); i++) {
            while (j > 0 && s.charAt(j) != s.charAt(i)) j = next[j - 1];
            if (s.charAt(j) == s.charAt(i)) j++;
            next[i] = j; 
        }
    }
}
```

时间复杂度：``O(n+m)``, 空间复杂度：``O(m)``

## 459.重复的子字符串
题目链接：[]()

思路：二刷的时候看！！！

答案：

```java

```

时间复杂度：``O()``, 空间复杂度：``O()``
