# 代码随想录算法训练营第二天（额外练习）| 88. Merge Sorted Array ，986. Interval List Intersections ，360. Sort Transformed Array
作者：Zhiwei Song 
日期：2023-06-02

## 88. Merge Sorted Array
题目链接： [https://leetcode.com/problems/merge-sorted-array/](https://leetcode.com/problems/merge-sorted-array/)

思路：这道题需要注意双指针pointer的位置，以及用``--i``还是``i--``.

答案：

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int pointer = m + n - 1;
        while (m > 0 && n > 0) {
            if (nums1[m-1] > nums2[n-1]) nums1[pointer--] = nums1[--m];
            else nums1[pointer--] = nums2[--n];
        }

        if (m == 0) {
            while (n > 0) nums1[pointer--] = nums2[--n];
        } else {
            while (m > 0) nums1[pointer--] = nums1[--m];
        }
    }
}
```

时间复杂度：``O(n+m)``, 空间复杂度：``O(1)``

## 986. Interval List Intersections

题目链接：[https://leetcode.com/problems/interval-list-intersections/](https://leetcode.com/problems/interval-list-intersections/)

思路：首先看两个interval有没有交集，然后看那个interval end在后面，就需要另一个interval count++。

答案：

```java
class Solution {
    public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
        int i = 0;
        int j = 0;
        List<int[]> result = new ArrayList<>();
        
        while (i < firstList.length && j < secondList.length) {
            if (Math.max(firstList[i][0], secondList[j][0]) 
            <= Math.min(firstList[i][1], secondList[j][1]))
                result.add(new int[]{Math.max(firstList[i][0], secondList[j][0]), Math.min(firstList[i][1], secondList[j][1])});
            
            if (firstList[i][1] > secondList[j][1]) j++;
            else i++;
        }

        return result.toArray(new int[result.size()][]);
    }
}
```

时间复杂度：``O(n+m)``, 空间复杂度：``O(n+m)``

## 360. Sort Transformed Array
题目链接：[https://leetcode.com/problems/sort-transformed-array](https://leetcode.com/problems/sort-transformed-array)

思路：这道题目是分为a大于0和a小于0来的判断，需要二刷。

答案：

```java
class Solution {
    public int[] sortTransformedArray(int[] nums, int a, int b, int c) {
        int[] result = new int[nums.length];
        int pointer = 0;
        int left = 0;
        int right = nums.length - 1;

        if (a >= 0) {
            while (left <= right) {
                int leftTransformedVal = transform(nums[left], a, b, c);
                int rightTransformedVal = transform(nums[right], a, b, c);
                if (leftTransformedVal > rightTransformedVal) {
                    result[pointer++] = leftTransformedVal;
                    left++;
                } else {
                    result[pointer++] = rightTransformedVal;
                    right--;
                }
            }

            for (int i = 0; i < nums.length / 2; i++) {
                int temp = result[i];
                result[i] = result[result.length - i - 1];
                result[result.length - i - 1] = temp;
            }
        } else {
            while (left <= right) {
                int leftTransformedVal = transform(nums[left], a, b, c);
                int rightTransformedVal = transform(nums[right], a, b, c);
                if (leftTransformedVal < rightTransformedVal) {
                    result[pointer++] = leftTransformedVal;
                    left++;
                } else {
                    result[pointer++] = rightTransformedVal;
                    right--;
                }
            }
        }

        return result;
    }

    private int transform(int x, int a, int b, int c) {
        return (a * x * x) + (b * x) + c;
    }
}
```

时间复杂度：``O(n+m)``, 空间复杂度：``O(n+m)``
