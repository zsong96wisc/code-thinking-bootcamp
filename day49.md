# 代码随想录算法训练营第四十九天| 309.最佳买卖股票时机含冷冻期 ， 714.买卖股票的最佳时机含手续费
作者：Zhiwei Song 
日期：2023-07-13

## 309.最佳买卖股票时机含冷冻期
题目链接：[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

思路：没有买入股票的话，跟前面几题是一样的。但是如果买入的话，是要看i - 2天的。把这个理清楚，需要二刷！

答案：

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) {
            return 0;
        }
        int[][] dp = new int[prices.length][2];

        // bad case
        dp[0][0] = 0;
        dp[0][1] = -prices[0];
        dp[1][0] = Math.max(dp[0][0], dp[0][1] + prices[1]);
        dp[1][1] = Math.max(dp[0][1], -prices[1]);

        for (int i = 2; i < prices.length; i++) {
            // dp公式
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] + prices[i]);
            dp[i][1] = Math.max(dp[i - 1][1], dp[i - 2][0] - prices[i]);
        }

        return dp[prices.length - 1][0];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 714.买卖股票的最佳时机含手续费
题目链接：[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

思路：跟前面几题不一样的地方在于卖出的时候要额外付个手续费。

答案：

```java
class Solution {
    public int maxProfit(int[] prices, int fee) {
        int[][] table = new int[prices.length][2];
        table[0][0] = 0;
        table[0][1] = -prices[0];

        for (int i = 1; i < prices.length; i++) {
            table[i][0] = Math.max(table[i - 1][0], table[i - 1][1] + prices[i] - fee);
            table[i][1] = Math.max(table[i - 1][1], table[i - 1][0] - prices[i]);
        }

        return table[table.length - 1][0];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
