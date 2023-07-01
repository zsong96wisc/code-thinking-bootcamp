# 代码随想录算法训练营第三十五天| 860.柠檬水找零 ，134. 加油站 ，45.跳跃游戏II
作者：Zhiwei Song 
日期：2023-06-27

## 860.柠檬水找零
题目链接：[https://leetcode.com/problems/lemonade-change/](https://leetcode.com/problems/lemonade-change/)

思路：先把5块钱的用了，因为它是万能的。

答案：

```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int five = 0;
        int ten = 0;

        for (int i = 0; i < bills.length; i++) {
            if (bills[i] == 5) five++;
            else if (bills[i] == 10) {
                ten++;
                five--;
                if (five < 0) return false;
            } else if (bills[i] == 20) {
                if (ten > 0 && five > 0) {
                    ten--;
                    five--;
                } else if (five > 2) five -= 3;
                else return false;
            }
        }
        return true;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 406.根据身高重建队列
题目链接：[https://leetcode.com/problems/queue-reconstruction-by-height/](https://leetcode.com/problems/queue-reconstruction-by-height/)

思路：先排大的人，在排小的人。可以用arraylist直接排。需要二刷！

答案：

```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, new Comparator<int[]>(){
            @Override
            public int compare(int[] a, int[] b) {
                if (a[0] == b[0]) return a[1] - b[1];
                return - (a[0] - b[0]);
            }
        });

        LinkedList<int[]> que = new LinkedList<>();

        for (int[] p : people) {
            que.add(p[1],p);
        }

        return que.toArray(new int[people.length][]);        
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 452. 用最少数量的箭引爆气球
题目链接：[https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/)

思路：根据末尾时间排队。

答案：

```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        Arrays.sort(points, new Comparator<int[]>(){
            @Override
            public int compare(int[] a, int[] b) {
                if (a[1] < b[1]) return -1;
                if (a[1] == b[1]) return 0;
                return 1;
            }
        });

        int end = points[0][1];
        int res = 1;
        for (int[] i : points) {
            if (i[0] > end) {
                res++;
                end = i[1];
            }
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

