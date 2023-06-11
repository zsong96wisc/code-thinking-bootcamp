# 代码随想录算法训练营第十八天| 513.找树左下角的值 ， 112. 路径总和 ， 113.路径总和ii 
作者：Zhiwei Song 
日期：2023-06-11

## 513.找树左下角的值
题目链接：[https://leetcode.com/problems/find-bottom-left-tree-value/](https://leetcode.com/problems/find-bottom-left-tree-value/)

思路：有递归的方法就是需要去首先遍历左边的child，然后要keep track最大的depth。如果最大的depth不变的话，说明当前记录的就是最左边的leaf。
迭代法就是层序遍历。需要二刷！

答案：

```java
class Solution {
    int maxDepth = Integer.MIN_VALUE;
    int result;
    public int findBottomLeftValue(TreeNode root) {
        if (root == null) return 0;
        recursion(root, 0);
        return result;
    }

    private void recursion(TreeNode node, int depth) {
        if (node.left == null && node.right == null) {
            if (depth > maxDepth) {
                maxDepth = depth;
                result = node.val;
            }
            return;
        }
        if (node.left != null) recursion(node.left, depth + 1);
        if (node.right != null) recursion(node.right, depth + 1);
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 112. 路径总和
题目链接：[https://leetcode.com/problems/path-sum/](https://leetcode.com/problems/path-sum/)

思路：递归，targetsum 减去当前值。

答案：

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;
        if (targetSum == root.val && root.left == null && root.right == null) return true;
        return hasPathSum(root.left, targetSum - root.val) || hasPathSum(root.right, targetSum - root.val);
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 113.路径总和ii
题目链接：[https://leetcode.com/problems/path-sum-ii/](https://leetcode.com/problems/path-sum-ii/)

思路：需要用一个list来记录当前path。要注意list存进去的时候要存copy。

答案：

```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> cur_list = new ArrayList<>();
        if (root == null) return res;
        else {
            cur_list.add(root.val);
            findPath(root, targetSum, cur_list, res);
        }
        return res;
    }

    private void findPath(TreeNode node, int targetSum, List<Integer> cur_list, List<List<Integer>> res) {
        if (node.left == null && node.right == null) {
            if (targetSum == node.val) {
                res.add(List.copyOf(cur_list));
            }
        } else {
            if (node.left != null) {
                cur_list.add(node.left.val);
                findPath(node.left, targetSum - node.val, cur_list, res);
                cur_list.remove(cur_list.size() - 1);
            } 
            if (node.right != null) {
                cur_list.add(node.right.val);
                findPath(node.right, targetSum - node.val, cur_list, res);
                cur_list.remove(cur_list.size() - 1);
            }
        }
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``
