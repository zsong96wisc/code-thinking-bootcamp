# 代码随想录算法训练营第八天| 344.反转字符串 ， 541. 反转字符串II ， 剑指Offer 05.替换空格 ， 151.翻转字符串里的单词 ， 剑指Offer58-II.左旋转字符串
作者：Zhiwei Song 
日期：2023-05-31

## 344.反转字符串
题目链接： [https://leetcode.com/problems/reverse-string/](https://leetcode.com/problems/reverse-string/)

思路：就是一遍loop，然后用额外的swap variable来翻转。

答案：

```java
class Solution {
    public void reverseString(char[] s) {
        for (int i = 0; i < s.length / 2; i++) {
            char swap = s[i];
            s[i] = s[s.length - 1 - i];
            s[s.length - 1 - i] = swap;
        }
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 541. 反转字符串II
题目链接：[https://leetcode.com/problems/reverse-string-ii/](https://leetcode.com/problems/reverse-string-ii/)

思路：看到了karl的讲解后，感觉自己写的代码复杂了。karl的代码是从前往后每一次增加2k，然后再进行判断。需要二刷用karl的方法。

答案：

```java
class Solution {
    public String reverseStr(String s, int k) {
        String[] result = s.split("");
        
        for (int i = 0; i <= s.length() / (2 * k); i++) {
            int startpos = i * 2 * k;
            if (i == s.length() / (2 * k) && s.length() - startpos < k) 
                reverse(result, startpos, s.length());
            else reverse(result, startpos, startpos + k);
        }

        return String.join("", result);
    }

    private void reverse(String[] result, int startpos, int endpos) {
        for (int i = 0; i < (endpos - startpos) / 2; i++) {
            String swap = result[startpos + i];
            result[startpos + i] = result[endpos - 1 - i];
            result[endpos - 1 - i] = swap;
        }
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 剑指Offer 05.替换空格
题目链接：[https://leetcode.cn/problems/ti-huan-kong-ge-lcof/](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

思路：karl的双指针的方法挺好的，把char array扩大到最后结果的长度，然后把空格替换掉。需要二刷，karl的方法。

答案：

```java
class Solution {
    public String replaceSpace(String s) {
        if (s == null) return s;

        StringBuilder result = new StringBuilder();
        for (char i : s.toCharArray()) {
            if (i == ' ') result.append("%20");
            else result.append(i);
        }
        return result.toString();
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 151.翻转字符串里的单词
题目链接：[https://leetcode.com/problems/reverse-words-in-a-string](https://leetcode.com/problems/reverse-words-in-a-string)

思路：详见karl的思路（https://programmercarl.com/0151.%E7%BF%BB%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%E9%87%8C%E7%9A%84%E5%8D%95%E8%AF%8D.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC）
虽然自己写出来了，但是下一次要学习karl的思路。需要二刷。

答案：

```java
class Solution {
    public String reverseWords(String s) {
        String[] result = new String[s.length()];
        int count = 0;
        int i = s.length() - 1;
        int j = s.length();

        while (j > 0) {
            if (i == -1 || s.charAt(i) == ' ') {
                if (i != s.length() - 1) result[count++] = s.substring(i + 1, j);
                while (i >= 0 && s.charAt(i) == ' ') i--;
                j = i;
                j++;
            } else {
                i--;
            }
        }
        return String.join(" ", Arrays.copyOfRange(result, 0, count));
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 剑指Offer58-II.左旋转字符串
题目链接：[https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

思路：参见了karl的思路 先反转前n 再反转后面剩下的 最后整体做一个反转。需要二刷。

答案：

```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        int len=s.length();
        StringBuilder sb=new StringBuilder(s);
        reverseString(sb,0,n-1);
        reverseString(sb,n,len-1);
        return sb.reverse().toString();
    }

    public void reverseString(StringBuilder sb, int start, int end) {
        while (start < end) {
            char temp = sb.charAt(start);
            sb.setCharAt(start, sb.charAt(end));
            sb.setCharAt(end, temp);
            start++;
            end--;
        }
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
