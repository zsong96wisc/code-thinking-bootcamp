# 代码随想录算法训练营第六天| 242.有效的字母异位词 ， 349. 两个数组的交集 ， 202. 快乐数 ， 1. 两数之和
作者：Zhiwei Song 
日期：2023-05-29

## 242. 有效的字母异位词
题目链接： [https://leetcode.com/problems/valid-anagram/](https://leetcode.com/problems/valid-anagram/)

思路：建立一个长度为26的数组作为哈希表。

答案：

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] table = new int[26];
        for (int i = 0; i < s.length(); i++) {
            table[s.charAt(i) - 'a'] += 1;
        }
        for (int i = 0; i < t.length(); i++) {
            if (--table[t.charAt(i) - 'a'] < 0) return false;
        }
        for (int i = 0; i < 26; i++) {
            if (table[i] > 0) return false;
        }
        return true;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 349. 两个数组的交集
题目链接：[https://leetcode.com/problems/intersection-of-two-arrays](https://leetcode.com/problems/intersection-of-two-arrays)

思路：用Hashset来保存A-list里面的unique的数值，然后跟B-list里面的数值一一对应。

答案：

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> occurance = new HashSet<>();
        HashSet<Integer> result = new HashSet<>();
        for (int i = 0; i < nums1.length; i++) {
            occurance.add(nums1[i]);
        }

        for (int i = 0; i < nums2.length; i++) {
            if (occurance.contains(nums2[i])) result.add(nums2[i]);
        }

        int[] results = new int[result.size()];
        int count = 0;
        for (int i : result) {
            results[count++] = i;
        }
        return results;
    }
}
```

时间复杂度：``O(n+m)``, 空间复杂度：``O(n+m)``

## 202. 快乐数
题目链接：[https://leetcode.com/problems/happy-number/](https://leetcode.com/problems/happy-number/)

思路：这道题目的精髓在于如果不是快乐数，每一步算出来的数字会循环重复出现。利用这个原理，用set解决。这道题是看了karl的讲解才做出来。需要二刷。
二刷时要注意时间和空间复杂度！！

答案：

```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> record = new HashSet<>();
        while (n != 1 && !record.contains(n)) {
            record.add(n);
            int res = 0;
            while (n > 0) {
                res += (n % 10) * (n % 10);
                n = n / 10;
            }
            n = res;
        }
        return n == 1;
    }
}
```

时间复杂度：``O(log(n))``, 空间复杂度：``O(log(n))``

## 1. 两数之和
题目链接：[https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/)

思路：用hashmap来存当前遇到过的数值。然后每次遇到新的数字。看看是不是前面hashmaps有的。

答案：

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++){
            if (map.containsKey(target - nums[i])){
                return new int[] {i, map.get(target - nums[i])};
            }
            map.put(nums[i], i);
        }
        return null;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

