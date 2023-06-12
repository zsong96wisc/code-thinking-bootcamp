# 代码随想录算法训练营第十八天| 654.最大二叉树 ， 617.合并二叉树 ， 700.二叉搜索树中的搜索 ， 98.验证二叉搜索树
作者：Zhiwei Song 
日期：2023-06-12

## 654.最大二叉树
题目链接：[https://leetcode.com/problems/maximum-binary-tree/](https://leetcode.com/problems/maximum-binary-tree/)

思路：递归思想。

答案：

```java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return helper(nums, 0, nums.length);
    }

    private TreeNode helper(int[] nums, int left, int right) {
        if (left == right) return null;
        int index = left;
        for (int i = left; i < right; i++) {
            if (nums[i] > nums[index]) index = i;
        }
        TreeNode root = new TreeNode(nums[index]);
        root.left = helper(nums, left, index);
        root.right = helper(nums, index + 1, right);
        return root;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 617.合并二叉树
题目链接：[https://leetcode.com/problems/merge-two-binary-trees/](https://leetcode.com/problems/merge-two-binary-trees/)

思路：如果一个树是null，则把下面的树都concat上去。

答案：

```java
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if (root1 == null) return root2;
        if (root2 == null) return root1;
        TreeNode root = new TreeNode(root1.val + root2.val);
        root.left = mergeTrees(root1.left, root2.left);
        root.right = mergeTrees(root1.right, root2.right);
        return root;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 700.二叉搜索树中的搜索 
题目链接：[https://leetcode.com/problems/search-in-a-binary-search-tree/](https://leetcode.com/problems/search-in-a-binary-search-tree/)

思路：需要掌握迭代法。

答案：

```java
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null) return null;
        if (root.val == val) return root;
        if (root.val < val) return searchBST(root.right, val);
        return searchBST(root.left, val);
    }
}
```

时间复杂度：``O(log(n))``, 空间复杂度：``O(log(n))``

## 98.验证二叉搜索树 
题目链接：[https://leetcode.com/problems/validate-binary-search-tree/](https://leetcode.com/problems/validate-binary-search-tree/)

思路：需要二刷。

答案：

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return helper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean helper(TreeNode node, long min_val, long max_val) {
        if (node == null) return true;
        if (node.val <= min_val || node.val >= max_val) return false;
        return helper(node.left, min_val, node.val)
            && helper(node.right, node.val, max_val);
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``
