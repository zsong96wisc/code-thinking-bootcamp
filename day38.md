# 代码随想录算法训练营第三十八天| 509. 斐波那契数 ，70. 爬楼梯 ，746. 使用最小花费爬楼梯 
作者：Zhiwei Song 
日期：2023-06-30

## 509. 斐波那契数
题目链接：[https://leetcode.com/problems/fibonacci-number/](https://leetcode.com/problems/fibonacci-number/)\

思路：简单题

答案：

```java
class Solution {
    public int fib(int n) {
        if (n < 2) return n;
        int[] res = new int[n + 1];
        res[0] = 0; res[1] = 1;
        for (int i = 2; i < n + 1; i++) {
            res[i] = res[i - 1] + res[i - 2];
        }
        return res[n];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 70. 爬楼梯 
题目链接：[https://leetcode.com/problems/climbing-stairs/](https://leetcode.com/problems/climbing-stairs/)

思路：经典dp 每一步是前两部小的数字+1

答案：

```java
class Solution {
    public int climbStairs(int n) {
        int[] steps = new int[n + 1];
        steps[0] = 1;
        steps[1] = 1;

        for (int i = 2; i < n + 1; i++) steps[i] = steps[i - 1] + steps[i - 2];

        return steps[n];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 746. 使用最小花费爬楼梯 
题目链接：[https://leetcode.com/problems/min-cost-climbing-stairs/](https://leetcode.com/problems/min-cost-climbing-stairs/)

思路：同70题爬楼梯

答案

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int[] res = new int[cost.length + 1];
        res[0] = 0;
        res[1] = 0;

        for (int i = 2; i < res.length; i++) {
            res[i] = Math.min(res[i - 2] + cost[i - 2], res[i - 1] + cost[i - 1]);
        }

        return res[res.length - 1];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
