# 代码随想录算法训练营第一天（额外练习2）| 896. Monotonic Array 、941. Valid Mountain Array ， 905. Sort Array By Parity ， 697. Degree of an Array ， 
# 1920. Build Array from Permutation

作者：Zhiwei Song 
日期：2023-06-04

## 896. Monotonic Array
题目链接： [https://leetcode.com/problems/monotonic-array/](https://leetcode.com/problems/monotonic-array/)

思路：这道题就是one-pass，如果既有increasing又有decreasing，则return false。

答案：

```java
class Solution {
    public boolean isMonotonic(int[] nums) {
        boolean pos = false;
        boolean neg = false;

        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i + 1] - nums[i] > 0) pos = true;
            if (nums[i + 1] - nums[i] < 0) neg = true;
            if (pos && neg) return false;
        }

        return true;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 941. Valid Mountain Array
题目链接：[https://leetcode.com/problems/valid-mountain-array/](https://leetcode.com/problems/valid-mountain-array/)

思路：这道题是借鉴tuttorial的，解题思路是模仿爬山，先下后上。

答案：

```java
class Solution {
    public boolean validMountainArray(int[] arr) {
        int position = 0;
        while (position < arr.length - 1) {
          if (arr[position + 1] == arr[position]) return false;
          else if (arr[position + 1] > arr[position]) position++;
          else break;
        }
        if (position == 0 || position == arr.length - 1) return false;

        while (position < arr.length - 1) {
          if (arr[position + 1] == arr[position]) return false;
          else if (arr[position + 1] < arr[position]) position++;
          else break;
        }
        return position == arr.length - 1 ? true : false;
        
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 905. Sort Array By Parity
题目链接：[https://leetcode.com/problems/sort-array-by-parity](https://leetcode.com/problems/sort-array-by-parity)

思路：双指针，注意edge case。下一次刷要考虑edge case，争取一次写对。需要二刷！

答案：

```java
class Solution {
    public int[] sortArrayByParity(int[] nums) {
        int count = nums.length - 1;
        int start = 0;
        
        while (count >= 0 && nums[count] % 2 == 1) count--;

        while (start < count && count >= 0 && start < nums.length) {
          if (nums[start] % 2 == 0) start++;
          else {
            int swap = nums[start];
            nums[start++] = nums[count];
            nums[count--] = swap;
            while (nums[count] % 2 == 1) count--;
          }
        }

        return nums;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 697. Degree of an Array
题目链接：[https://leetcode.com/problems/degree-of-an-array/](https://leetcode.com/problems/sort-array-by-parity](https://leetcode.com/problems/degree-of-an-array/)

思路：注意什么时候更新minlen和maxocc。需要二刷！

答案：

```java
class Solution {
    public int findShortestSubArray(int[] nums) {
        HashMap<Integer, int[]> maps = new HashMap<>();
        int minlen = 0;
        int maxocc = 0;

        for (int i = 0; i < nums.length; i++) {
          if (!maps.containsKey(nums[i])) maps.put(nums[i], new int[]{i, 1});
          else maps.get(nums[i])[1] += 1;

          if (maps.get(nums[i])[1] > maxocc) {
            maxocc = maps.get(nums[i])[1];
            minlen = i - maps.get(nums[i])[0];
          } else if (maps.get(nums[i])[1] == maxocc) {
            if (i - maps.get(nums[i])[0] < minlen) minlen = i - maps.get(nums[i])[0];
          }
        }

        return minlen + 1;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 1920. Build Array from Permutation
题目链接：[https://leetcode.com/problems/build-array-from-permutation/](https://leetcode.com/problems/build-array-from-permutation/)

思路：学习recursive方法

答案：

```java
class Solution {
    public int[] buildArray(int[] nums) {
        int [] ans = new int [nums.length];
        for(int i =0;i<nums.length;i++) {
            ans[i] = nums[nums[i]];
        }
        return ans;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``



