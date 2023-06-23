# 代码随想录算法训练营第三十一天| 455.分发饼干 ，376. 摆动序列 ，53. 最大子序和
作者：Zhiwei Song 
日期：2023-06-23

## 455.分发饼干
题目链接：[https://leetcode.com/problems/assign-cookies/](https://leetcode.com/problems/assign-cookies/)

思路：简单greedy。

答案：

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int i = 0; int j = 0;

        while (i < g.length && j < s.length) {
            if (g[i] <= s[j]) {
                i++;
                j++;
            } else j++;
        }
        return i;
    }
}
```

时间复杂度：``O(n+m)``, 空间复杂度：``O(1)``

## 376. 摆动序列
题目链接：[https://leetcode.com/problems/wiggle-subsequence/](https://leetcode.com/problems/wiggle-subsequence/)

思路：看了karl的解法，需要二刷。

答案：

```java
class Solution {
    public int wiggleMaxLength(int[] nums) {
        if (nums.length <= 1) return nums.length;
        int prediff = 0;
        int curdiff = 0;
        int result = 1;

        for (int i = 0; i < nums.length - 1; i++) {
            curdiff = nums[i + 1] - nums[i];
            if ((prediff >= 0 && curdiff < 0) || (prediff <= 0 && curdiff > 0)){
                result++;
                prediff = curdiff;
            }
        }

        return result;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 53. 最大子序和
题目链接：[https://leetcode.com/problems/maximum-subarray/](https://leetcode.com/problems/maximum-subarray/)

思路：遇到0或者负数就重开。

答案：

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int max = Integer.MIN_VALUE;
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            if (sum < 0) {
                sum = 0;
            }
            sum += nums[i];
            if (sum > max) {
                max = sum;
            }
        }
        return max;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

