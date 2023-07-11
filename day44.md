# 代码随想录算法训练营第四十四天| 70. 爬楼梯 （进阶） ， 322. 零钱兑换 ，279.完全平方数
作者：Zhiwei Song 
日期：2023-07-07

## 70. 爬楼梯 （进阶）
题目链接：[https://leetcode.com/problems/climbing-stairs/](https://leetcode.com/problems/climbing-stairs/)

思路：完全背包就是每一个物品都可以放无限次。所以我们要从前往后遍历。如果先遍历物品，物品放入顺序就是固定的。

答案：

```java
class Solution {
    public int climbStairs(int n) {
        int[] table = new int[n + 1];
        table[0] = 1;
        for (int i = 0; i < n + 1; i++) {
            for (int j = 1; j < 3; j++) {
                if (i >= j) table[i] += table[i - j];
            }
        }
        return table[n];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``

## 322. 零钱兑换
题目链接：[https://leetcode.com/problems/coin-change/](https://leetcode.com/problems/coin-change/)

思路：完全背包。每次做多只能用amount个硬币，所以把所有的数值都设置成amount+1。然后完全背包就是存多少个硬币。

答案：

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] table = new int[amount + 1];
        table[0] = 0;
        for (int j = 1; j < amount + 1; j++) table[j] = amount + 1;
        for (int i = 0; i < coins.length; i++) {
            for (int j = 1; j < amount + 1; j++) {
                if (j >= coins[i]) table[j] = Math.min(table[j], table[j - coins[i]] + 1);
            }
        }
        return table[amount] == amount + 1 ? -1 : table[amount];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``

## 279.完全平方数
题目链接：[https://leetcode.com/problems/perfect-squares/](https://leetcode.com/problems/perfect-squares/)

思路：完全背包。

答案：

```java
class Solution {
    public int numSquares(int n) {
        int[] table = new int[n + 1];
        table[1] = 1;
        for (int i = 2; i < n + 1; i++) {
            int min = n + 1;
            for (int j = 1; j <= i / 2; j++) {
                if (j * j <= i) min = Math.min(table[i - j * j] + 1, min);
            }
            table[i] = min;
        }
        return table[n];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``
