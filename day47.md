# 代码随想录算法训练营第四十七天| 121. 买卖股票的最佳时机 ， 122.买卖股票的最佳时机II
作者：Zhiwei Song 
日期：2023-07-11

## 121. 买卖股票的最佳时机
题目链接：[https://leetcode.com/problems/best-time-to-buy-and-sell-stock/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

思路：每次买进的时候，都是`-prices[i]`的收入。

答案：

```java
class Solution {
    public int maxProfit(int[] prices) {
        int[][] table = new int[prices.length][2];
        table[0][0] = -prices[0];
        table[0][1] = 0;
        for (int i = 1; i < prices.length; i++) {
            table[i][0] = Math.max(table[i - 1][0], -prices[i]);
            table[i][1] = Math.max(table[i - 1][1], table[i - 1][0] + prices[i]);
        }
        return Math.max(table[prices.length - 1][0], table[prices.length - 1][1]);
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``

## 122.买卖股票的最佳时机II
题目链接：[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

思路：这个跟上一题的区别在于买入的时候是`table[i - 1][1] - prices[i]`。

答案：

```java
class Solution {
    public int maxProfit(int[] prices) {
        int[][] table = new int[prices.length][2];
        table[0][0] = -prices[0];
        table[0][1] = 0;
        for (int i = 1; i < prices.length; i++) {
            table[i][0] = Math.max(table[i - 1][0], table[i - 1][1] - prices[i]);
            table[i][1] = Math.max(table[i - 1][1], table[i - 1][0] + prices[i]);
        }
        return Math.max(table[prices.length - 1][0], table[prices.length - 1][1]);
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``
