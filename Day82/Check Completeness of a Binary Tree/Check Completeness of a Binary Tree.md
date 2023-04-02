# 958. Check Completeness of a Binary Tree

Given the `root` of a binary tree, determine if it is a complete binary tree.

In a complete binary tree, every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between `1` and `2h` nodes inclusive at the last level `h`.

**Example 1:**

<img src="https://assets.leetcode.com/uploads/2018/12/15/complete-binary-tree-1.png" alt="img" style="height: 200px; width: 200px;"/>

```
Input: root = [1,2,3,4,5,6]
Output: true
Explanation: Every level before the last is full (ie. levels with node-values {1} and {2, 3}), and all nodes in the last level ({4, 5, 6}) are as far left as possible.
```
**Example 2:**

<img src="https://assets.leetcode.com/uploads/2018/12/15/complete-binary-tree-2.png" alt="img" style="height: 200px; width: 200px;"/>

```
Input: root = [1,2,3,4,5,null,7]
Output: false
Explanation: The node with value 7 isn't as far left as possible.
``` 

**Constraints:**

* The number of nodes in the tree is in the range `[1, 100]`.
* `1 <= Node.val <= 1000`

**Solution:**
```
class Solution {
  public boolean isCompleteTree(TreeNode root) {
    if (root == null)
      return true;

    Queue<TreeNode> q = new LinkedList<>(Arrays.asList(root));

    while (q.peek() != null) {
      TreeNode node = q.poll();
      q.offer(node.left);
      q.offer(node.right);
    }

    while (!q.isEmpty() && q.peek() == null)
      q.poll();

    return q.isEmpty();
  }
}
```