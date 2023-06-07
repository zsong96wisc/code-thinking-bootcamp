# 代码随想录算法训练营第十四天| 144. Binary Tree Preorder Traversal ， 145. Binary Tree Postorder Traversal ， 94. Binary Tree Inorder Traversal 
作者：Zhiwei Song 
日期：2023-06-06

## 144. Binary Tree Preorder Traversal
题目链接： [https://leetcode.com/problems/binary-tree-preorder-traversal/](https://leetcode.com/problems/binary-tree-preorder-traversal/)

思路：学习了Karl的前序遍历用Stack的方式来写，需要二刷。

答案：

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> res = new ArrayList<>();

        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode cur = stack.pop();
            if (cur == null) continue;
            else {
                res.add(cur.val);
                stack.push(cur.right);
                stack.push(cur.left);
            }
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 145. Binary Tree Postorder Traversal
题目链接：[https://leetcode.com/problems/binary-tree-postorder-traversal/](https://leetcode.com/problems/binary-tree-postorder-traversal/)

思路：学习了Karl的后序遍历用Stack的方式来写，需要二刷。

答案：

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();

        stack.add(root);
        while (!stack.isEmpty()) {
            TreeNode cur = stack.pop();
            if (cur == null) continue;
            else {
                res.add(cur.val);
                stack.push(cur.left);
                stack.push(cur.right);
            }
        }

        Collections.reverse(res);
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 94. Binary Tree Inorder Traversal
题目链接：[https://leetcode.com/problems/binary-tree-inorder-traversal/](https://leetcode.com/problems/binary-tree-inorder-traversal/)

思路：学习了Karl的中序遍历用Stack的方式来写，需要二刷。

答案：

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> res = new ArrayList<>();
        TreeNode cur = root;

        while (!stack.isEmpty() || cur != null) {
            if (cur != null) {
                stack.push(cur);
                cur = cur.left;
            } else {
                cur = stack.pop();
                    res.add(cur.val);
                    cur = cur.right;
            }
        }

        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``
