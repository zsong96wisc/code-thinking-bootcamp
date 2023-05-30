# 代码随想录算法训练营第七天| 454.四数相加II ， 383. 赎金信 ， 15. 三数之和 ， 18. 四数之和
作者：Zhiwei Song 
日期：2023-05-30

## 454.四数相加II
题目链接： [https://leetcode.com/problems/4sum-ii/](https://leetcode.com/problems/4sum-ii/)

思路：要学会利用map的特性，像两数之和的那样，for循环前两个list，把``a+b``的之和存到map里面。
然后再循环cd list来判断是不是有在map里面遇到的。这道题不难的点在于不用去重，因为每一个数值的index是不一样的。
相比于三数之和和四数之和的题目，这道题可以用哈希表来解决。需要二刷。

答案：

```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        Map<Integer, Integer> map = new HashMap<>();
        int count = 0;

        for (int i = 0; i < nums1.length; i++){
            for (int j = 0; j < nums2.length; j++){
                map.put(nums1[i] + nums2[j], map.getOrDefault(nums1[i] + nums2[j], 0) + 1);
            }
        }
        for (int i = 0; i < nums3.length; i++){
            for (int j = 0; j < nums4.length; j++){
                count += map.getOrDefault(-nums3[i] - nums4[j], 0);
            }
        }

        return count;
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n^2)``

## 383. 赎金信
题目链接：[https://leetcode.com/problems/ransom-note/](https://leetcode.com/problems/ransom-note/)

思路：这个思路跟242题目是一样的。

答案：

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int[] hashtable = new int[26];

        for (int i = 0; i < magazine.length(); i++) {
            hashtable[magazine.charAt(i) - 'a']++;
        }

        for (int i = 0; i < ransomNote.length(); i++) {
            if (--hashtable[ransomNote.charAt(i) - 'a'] < 0) return false;
        }

        return true;
    }
}
```

时间复杂度：``O(m)``, 空间复杂度：``O(1)``

## 15. 三数之和
题目链接：[https://leetcode.com/problems/3sum/](https://leetcode.com/problems/3sum/)

思路：见carl的代码随想录：https://programmercarl.com/0015.%E4%B8%89%E6%95%B0%E4%B9%8B%E5%92%8C.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC。 需要二刷！

答案：

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            if (i != 0 && nums[i-1] == nums[i]) continue;
            
            int left = i + 1;
            int right = nums.length - 1;

            while (right > left) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum > 0) {
                    right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    while (right > left && nums[right] == nums[right - 1]) right--;
                    while (right > left && nums[left] == nums[left + 1]) left++;
                    
                    right--; 
                    left++;
                }
            }
        }
        return result;
    }
}
```

时间复杂度：``O(nlog(n) + n^2)``, 空间复杂度：``O(log(n))``

## 18. 四数之和
题目链接：[https://leetcode.com/problems/4sum/](https://leetcode.com/problems/4sum/)

思路：见carl的代码随想录：https://programmercarl.com/0018.%E5%9B%9B%E6%95%B0%E4%B9%8B%E5%92%8C.html#%E8%A1%A5%E5%85%85。 需要二刷！

答案：

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);
       
        for (int i = 0; i < nums.length; i++) {
		
            // nums[i] > target 直接返回, 剪枝操作
            if (nums[i] > 0 && nums[i] > target) {
                return result;
            }
		
            if (i > 0 && nums[i - 1] == nums[i]) {    // 对nums[i]去重
                continue;
            }
            
            for (int j = i + 1; j < nums.length; j++) {

                if (j > i + 1 && nums[j - 1] == nums[j]) {  // 对nums[j]去重
                    continue;
                }

                int left = j + 1;
                int right = nums.length - 1;
                while (right > left) {
		    // nums[k] + nums[i] + nums[left] + nums[right] > target int会溢出
                    long sum = (long) nums[i] + nums[j] + nums[left] + nums[right];
                    if (sum > target) {
                        right--;
                    } else if (sum < target) {
                        left++;
                    } else {
                        result.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
                        // 对nums[left]和nums[right]去重
                        while (right > left && nums[right] == nums[right - 1]) right--;
                        while (right > left && nums[left] == nums[left + 1]) left++;

                        left++;
                        right--;
                    }
                }
            }
        }
        return result;
    }
}
```

时间复杂度：``O(n^3)``, 空间复杂度：``O(log(n))``

