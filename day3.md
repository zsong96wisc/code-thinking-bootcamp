# 代码随想录算法训练营第三天| 203.移除链表元素 ， 707.设计链表 ， 206.反转链表
作者：Zhiwei Song 
日期：2023-05-26

## 203.移除链表元素
题目链接： [https://leetcode.com/problems/remove-linked-list-elements/](https://leetcode.com/problems/remove-linked-list-elements/)

思路：这道题目要注意如果下一个节点被删掉了，就不要把head的指针向前移一位。

答案：

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummynode = new ListNode(0, head);
        head = dummynode;
        while (head.next != null){
            if (head.next.val == val){
                head.next = head.next.next;
            } else {
                head = head.next;
            }
        }
        return dummynode.next;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 707.设计链表
题目链接：[https://leetcode.com/problems/design-linked-list/](https://leetcode.com/problems/design-linked-list/)

思路：这道题考验linkedlist基础构架，需要二刷。

答案：

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(){}
    ListNode(int val){
        this.val = val;
    }
    ListNode(int val, ListNode next){
        this.val = val;
        this.next = next;
    }
}

class MyLinkedList {
    int size;
    ListNode head;

    public MyLinkedList() {
        this.size = 0;
        head = new ListNode(0);
    }
    
    public int get(int index) {
        if (index < 0 || index >= size) return -1;
        ListNode currnode = head;
        for (int i = 0; i<= index; i++){
            currnode = currnode.next;
        }
        return currnode.val;
    }
    
    public void addAtHead(int val) {
        addAtIndex(0, val);
    }
    
    public void addAtTail(int val) {
        addAtIndex(size, val); 
    }
    
    public void addAtIndex(int index, int val) {
        if (index > size) return;;
        if (index < 0) index = 0;

        size++;

        ListNode currnode = head;
        for (int i = 0; i < index; i++){
            currnode = currnode.next;
        }

        ListNode newnode = new ListNode(val, currnode.next);
        currnode.next = newnode;
    }
    
    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }

        size--;

        if (index == 0){
            head = head.next;
            return;
        }

        ListNode currnode = head;
        for (int i = 0; i < index ; i++) {
            currnode = currnode.next;
        }
        currnode.next = currnode.next.next;
    }
}
```

时间复杂度：``O()``, 空间复杂度：``O()``

## 206.反转链表
题目链接：[https://leetcode.com/problems/spiral-matrix-ii/](https://leetcode.com/problems/spiral-matrix-ii/)

思路：这道题要存当前的指针前一个节点和后一个节点。比较典型。

答案：

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null) return null;
        ListNode pre = null;

        while (head != null){
            ListNode nex = head.next;
            head.next = pre;
            pre = head;
            head = nex;
        }
        return pre;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
