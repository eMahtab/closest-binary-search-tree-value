# Closest Binary Search Tree Value
## https://leetcode.com/problems/closest-binary-search-tree-value

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

**Note:**
1. Given target value is a floating point.
2. You are guaranteed to have only one unique value in the BST that is closest to the target.
```
Example:

Input: root = [4,2,5,1,3], target = 3.714286

    4
   / \
  2   5
 / \
1   3

Output: 4

But if target is 3.5 and we are asked to return the smallest number which is closest to target,
then answer will be 3 and not 4 (both 3 and 4 have the same difference from target but 3 is smaller than 4) .
```
# Implementation 1 : O(nlogn), inorder traversal, sort 
```java
class Solution {
  public int closestValue(TreeNode root, double target) {
    List<Integer> nums = new ArrayList();
    inorder(root, nums);
    Collections.sort(nums, (n1,n2) -> 
                      Double.compare(Math.abs(n1 - target), Math.abs(n2 - target)));
    return nums.get(0);
  }

  public void inorder(TreeNode node, List<Integer> nums) {
    if (node == null) return;
    inorder(node.left, nums);
    nums.add(node.val);
    inorder(node.right, nums);
  }
}
```

# Implementation 2 : O(h)

```java
class Solution {
    public int closestValue(TreeNode root, double target) {
        int closestValue = root.val;
        TreeNode node = root;
        while(node != null){
            if(Math.abs(node.val - target) < Math.abs(closestValue - target))
                closestValue = node.val;
            node = target < node.val ? node.left : node.right;
        }
        return closestValue;
    }
}
```
# Implementation 3 : O(h), If there are multiple answers, return the smallest number
```java
class Solution {
    public int closestValue(TreeNode root, double target) {
        int closestValue = root.val;
        TreeNode node = root;
        while(node != null){
            if(Math.abs(node.val - target) < Math.abs(closestValue - target) ||
               (Math.abs(node.val - target) == Math.abs(closestValue - target) && node.val < closestValue))
                closestValue = node.val;
            node = target < node.val ? node.left : node.right;
        }
        return closestValue;
    }
}
```

# References :
https://www.youtube.com/watch?v=_sz0Y4g1Gos
https://leetcode.com/problems/closest-binary-search-tree-value/editorial
