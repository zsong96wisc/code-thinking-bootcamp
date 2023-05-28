# 代码随想录算法训练营第四天| 24. 两两交换链表中的节点 ， 19.删除链表的倒数第N个节点 ， 面试题 02.07. 链表相交 ， 142.环形链表II
作者：Zhiwei Song 
日期：2023-05-27

## 24. 两两交换链表中的节点
题目链接： [https://leetcode.com/problems/swap-nodes-in-pairs/description/](https://leetcode.com/problems/swap-nodes-in-pairs/description/)

思路：这道题的重点在于画图，怎么去改变节点的下一个节点，以及在节点边界问题上的处理。自己做出来啦！

答案：

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummynode = new ListNode(0, head);
        ListNode curnode = dummynode;

        while (curnode != null && curnode.next != null) {
            if (curnode.next.next == null) break;
            ListNode nextnode = curnode.next;
            curnode.next = curnode.next.next;
            nextnode.next = nextnode.next.next;
            curnode.next.next = nextnode;
            curnode = nextnode;
        }

        return dummynode.next;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 19.删除链表的倒数第N个节点
题目链接：[https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

思路：快慢双指针，判断边界问题。自己做出来啦！

答案：

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummynode = new ListNode(0, head);
        ListNode fastnode = dummynode;
        ListNode slownode = dummynode;

        while (n > 0 && fastnode != null){
            fastnode = fastnode.next;
            n--;
        }

        if (n != 0) return null;

        while (fastnode.next != null) {
            fastnode = fastnode.next;
            slownode = slownode.next;
        }

        slownode.next = slownode.next.next;
        return dummynode.next;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 面试题 02.07. 链表相交
题目链接：[https://leetcode.com/problems/intersection-of-two-linked-lists/](https://leetcode.com/problems/intersection-of-two-linked-lists/)

思路：copy了karl的思路(https://programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)。需要二刷。

答案：

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode curA = headA;
        ListNode curB = headB;
        int lenA = 0;
        int lenB = 0;

        while (curA != null){
            lenA++;
            curA = curA.next;
        }

        while (curB != null){
            lenB++;
            curB = curB.next;
        }

        curA = headA;
        curB = headB;

        if (lenB > lenA){
            int swapi = lenB;
            lenB = lenA;
            lenA = swapi;
            ListNode swapn = curB;
            curB = curA;
            curA = swapn;
        }

        int gap = lenA - lenB;
        while (gap-- > 0) curA = curA.next;

        while (curA != null) {
            if (curA == curB) {
                return curA;
            }
            curA = curA.next;
            curB = curB.next;
        }
        return null;
    }
}
```

时间复杂度：``O(m+n)``, 空间复杂度：``O(1)``

## 142.环形链表II
题目链接：[https://leetcode.com/problems/linked-list-cycle-ii/description/](https://leetcode.com/problems/linked-list-cycle-ii/description/)

思路：画图来理解每段长度之间的关系。

答案：

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        boolean cycle = false;

        while (fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                cycle = true;
                break;
            }
        }

        if (!cycle) return null;
        else {
            slow = head;
            while (slow != fast){
                slow = slow.next;
                fast = fast.next;
            }
            return slow;
        }
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

