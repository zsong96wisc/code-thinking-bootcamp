# 代码随想录算法训练营第二十二天| 235. 二叉搜索树的最近公共祖先 ， 701.二叉搜索树中的插入操作 ， 450.删除二叉搜索树中的节点 
作者：Zhiwei Song 
日期：2023-06-14

## 235. 二叉搜索树的最近公共祖先
题目链接：[https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

思路：这道题借鉴了karl的思路，利用了搜索二叉树的特性。如果当前node的val是在p，q中间，那它一定是最近公共祖先。可以二刷重新思考靠这个点！

答案：

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root.val > p.val && root.val > q.val)
            return lowestCommonAncestor(root.left, p, q);
        else if (root.val < p.val && root.val < q.val)
            return lowestCommonAncestor(root.right, p, q);
        return root;
    }
}
```

时间复杂度：``O(log(n))``, 空间复杂度：``O(log(n))``

## 701.二叉搜索树中的插入操作 
题目链接：[https://leetcode.com/problems/insert-into-a-binary-search-tree/](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

思路：搜索二叉树插入节点只能插在leaf上面。

答案：

```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) return new TreeNode(val);
        if (root.val > val) root.left = insertIntoBST(root.left, val);
        else root.right = insertIntoBST(root.right, val);
        return root;
    }
}
```

时间复杂度：``O(log(n))``, 空间复杂度：``O(log(n))``

## 450.删除二叉搜索树中的节点
题目链接：[https://leetcode.com/problems/delete-node-in-a-bst/](https://leetcode.com/problems/delete-node-in-a-bst/)

思路：删除分三种情况，本身是leaf，自己只有一个child，自己有两个child，那就用左最大或右最小来替代。

答案：

```java
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return null;
        if (root.val == key) {
            if (root.left == null && root.right == null) return null;
            else if (root.left == null) return root.right;
            else if (root.right == null) return root.left;
            TreeNode cur = root.right;
            while (cur.left != null) cur = cur.left;
            root.val = cur.val;
            root.right = deleteNode(root.right, cur.val);
            return root;
        } else if (root.val > key) {
            root.left = deleteNode(root.left, key);
            return root;
        } else {
            root.right = deleteNode(root.right, key);
            return root;
        }

    }
}
```

时间复杂度：``O(log(n))``, 空间复杂度：``O(log(n))``
