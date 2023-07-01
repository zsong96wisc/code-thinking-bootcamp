# 代码随想录算法训练营第三十六天| 860.柠檬水找零 ，763.划分字母区间 ，56. 合并区间
作者：Zhiwei Song 
日期：2023-06-28

## 435. 无重叠区间 
题目链接：[https://leetcode.com/problems/non-overlapping-intervals/](https://leetcode.com/problems/non-overlapping-intervals/)

思路：按照终止时间sort这个array。

答案：

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[1], b[1]));
        int end = intervals[0][1];
        int result = 1;
        for (int[] i : intervals) {
            if (i[0] >= end) {
                end = i[1];
                result++;
            }
        }
        return intervals.length - result;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 763.划分字母区间
题目链接：[https://leetcode.com/problems/partition-labels/](https://leetcode.com/problems/partition-labels/)

思路：从前往后遍历，然后如果遍历过后两个pointer相遇了，就停止切出来。
答案：

```java
class Solution {
    public List<Integer> partitionLabels(String s) {
        List<Integer> res = new ArrayList<>();
        int[] intervals = new int[26];
        for (int i = 0; i < s.length(); i++) {
            intervals[s.charAt(i) - 'a'] = i;
        }
        
        int end = 0;
        int start = 0;
        for (int i = 0; i < s.length(); i++) {
            end = Math.max(end, intervals[s.charAt(i) - 'a']);
            if (i == end) {
                res.add(i - start + 1);
                start = i + 1;
            }
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 56. 合并区间
题目链接：[https://leetcode.com/problems/merge-intervals/](https://leetcode.com/problems/merge-intervals/)
思路：根据末尾时间排队。

答案：根据interval的开始时间来估计多少个interval。

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        List<int[]> res = new ArrayList<>();
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        int start = intervals[0][0];
        int end = intervals[0][1];

        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] > end) {
                res.add(new int[]{start, end});
                start = intervals[i][0];
                end = intervals[i][1];
            } else {
                end = Math.max(end, intervals[i][1]);
            }
        }
        res.add(new int[]{start, end});
        int[][] result = new int[res.size()][2];
        return res.toArray(result);
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

