# 代码随想录算法训练营第十一天| 20. 有效的括号 ， 1047. 删除字符串中的所有相邻重复项 ， 150. 逆波兰表达式求值 
作者：Zhiwei Song 
日期：2023-06-03

## 20. 有效的括号
题目链接： [https://leetcode.com/problems/valid-parentheses/](https://leetcode.com/problems/valid-parentheses/)

思路：注意java里面stack和deque的区别。下一次写的时候可以使用deque来写。

答案：

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();

        for (char chr : s.toCharArray()) {
            if (chr == '(') stack.add(')');
            else if (chr == '{') stack.add('}');
            else if (chr == '[') stack.add(']');
            else {
                if (stack.isEmpty() || chr != stack.pop()) {
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 1047. 删除字符串中的所有相邻重复项
题目链接：[https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)

思路：用stack来记住每个position的前一个位置上是什么值。

答案：

```java
class Solution {
    public String removeDuplicates(String s) {
        Deque<Character> deque = new LinkedList<>();

        for (char chr : s.toCharArray()) {
            if (deque.isEmpty()) deque.addLast(chr);
            else {
                if (deque.peekLast() != chr) deque.addLast(chr);
                else deque.removeLast();
            }
        }

        char[] result = new char[deque.size()];
        int count = 0;
        while (!deque.isEmpty()) result[count++] = deque.removeFirst();

        return new String(result);
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 150. 逆波兰表达式求值
题目链接：[https://leetcode.com/problems/evaluate-reverse-polish-notation/](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

思路：用stack来track表达式，而且这道题不用去evaluate表达式是不是valid。

答案：

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Deque<Integer> deque = new LinkedList<>();

        for (String chr : tokens) {
            if (chr.equals("+")) {
                deque.addLast(deque.removeLast() + deque.removeLast());
            } else if (chr.equals("-")) {
                deque.addLast(-deque.removeLast() + deque.removeLast());
            } else if (chr.equals("*")) {
                deque.addLast(deque.removeLast() * deque.removeLast());
            } else if (chr.equals("/")) {
                int secondnum = deque.removeLast();
                int firstnum = deque.removeLast();
                deque.addLast(firstnum / secondnum);
            } else deque.addLast(Integer.parseInt(chr));
        }

        return deque.removeLast();
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``
