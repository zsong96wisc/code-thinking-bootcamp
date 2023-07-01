# 代码随想录算法训练营第三十九天| 62.不同路径 ，63. 不同路径 II
作者：Zhiwei Song 
日期：2023-07-01

## 62.不同路径
题目链接：[https://leetcode.com/problems/unique-paths/](https://leetcode.com/problems/unique-paths/)

思路：小学奥数题，注意边都是1。

答案：

```java
class Solution {
    public int uniquePaths(int m, int n) {
        if (m == 1 || n == 1) return 1;
        int[][] table = new int[m][n];
        for (int i = 0; i < n; i++) table[0][i] = 1;
        for (int i = 0; i < m; i++) table[i][0] = 1;
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                table[i][j] = table[i - 1][j] + table[i][j - 1];
            }
        }
        return table[m - 1][n - 1];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 63. 不同路径 II
题目链接：[https://leetcode.com/problems/unique-paths-ii/](https://leetcode.com/problems/unique-paths-ii/)

思路：注意障碍就是0，以及如果一开始就是0。

答案：

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int fill = 1;
        for (int i = 0; i < n; i++) {
            if (obstacleGrid[0][i] == 1) fill = 0;
            obstacleGrid[0][i] = fill;
        }
        fill = obstacleGrid[0][0];
        for (int i = 1; i < m; i++) {
            if (obstacleGrid[i][0] == 1) fill = 0;
            obstacleGrid[i][0] = fill;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (obstacleGrid[i][j] == 1) obstacleGrid[i][j] = 0;
                else obstacleGrid[i][j] = obstacleGrid[i - 1][j] + obstacleGrid[i][j - 1];
            }
        }
        return obstacleGrid[m - 1][n - 1];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
