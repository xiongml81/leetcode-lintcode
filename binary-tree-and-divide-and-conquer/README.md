# Binary Tree and Divide & Conquer 二叉树和分治法

**1.Divide & Conquer (D & C)**

Divide big problem into several similar and smaller problems** **\
****D\&C vs. Binary Search

* Assime the process time is O(1)
* Divide & Conquer needs to process for both sides after the divide. O(n)
* Binary Search throws away half side after the divide O(log n)
* Array (divide big array into disjoint subarrays)
* Linked List (not that good, need to O(n) to find the cutting point)
* Binary Tree (most natural, it has left and right sub-tree)

Most Binary tree questions could be solved by Divide & Conquer

A few Concepts about search

Recursions, DFS, Backtracking, Traversal, D\&C, Iteration

Search by orders (depth first or breadth first)

Backtracking is the step where we recover all the states when going back for a new forking - some times we need to manually recover the state, and in recursion, there is also automatic recovering of state when we come to the upper layer of stack of the OS. Thus in certain sense, DFS must has backtracking and they are equivalent.\
\
Different algorithm (take different route) for DFS: traversal vs D\&C

Different implementation (drive or walk) for traversal or D\&C:\
recursion vs. iteration

![](<../.gitbook/assets/image (3).png>)

**2. Binary Tree**

Consider: root, leaf, node in the middle (substree), and null node

Find value/path in a Binary Tree (DFS)

How many subtrees are there in a binary tree? O(n) - all the nodes in the tree\


![](<../.gitbook/assets/image (5).png>)

Binary Tree Traversal

in order\
[https://leetcode.com/problems/binary-tree-inorder-traversal/](https://leetcode.com/problems/binary-tree-inorder-traversal/)

```
        if(root == null){
            return res;
        }
        
        inorderTraversal(root.left);
        res.add(root.val);
        inorderTraversal(root.right);
```

post order\
[https://leetcode.com/problems/binary-tree-postorder-traversal/](https://leetcode.com/problems/binary-tree-postorder-traversal/)

```
       if(root == null){
            return res;
        }
        
        inorderTraversal(root.left);
        inorderTraversal(root.right);
        res.add(root.val);
```

pre order\
[https://leetcode.com/problems/binary-tree-preorder-traversal/](https://leetcode.com/problems/binary-tree-preorder-traversal/)

```
         if(root == null){
            return res;
        }
        res.add(root.val);
        inorderTraversal(root.left);
        inorderTraversal(root.right);
```

level order\
[https://leetcode.com/problems/binary-tree-level-order-traversal/](https://leetcode.com/problems/binary-tree-level-order-traversal/)

```
        if(root == null){
            return res;
        }
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty()){
            List<Integer> temp = new ArrayList<>();
            int size = queue.size();
            for(int i = 0; i < size; i++){
                TreeNode level = queue.poll();
                temp.add(level.val);
                if(level.left != null){
                    queue.offer(level.left);
                }
                if(level.right != null){
                    queue.offer(level.right);
                }
            }
            res.add(temp);
            
        }
```

zigzag order

[https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

```
        if(root == null){
            return res;
        }
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        boolean left2right = true;
        while(!queue.isEmpty()){
            List<Integer> temp = new ArrayList<>();
            int size = queue.size();
            
            for(int i = 0; i < size; i++){
                
                TreeNode level = queue.poll();
                if(left2right == true){
                    temp.add(level.val);
                }
                else{
                    temp.add(0, level.val);
                }
                
                if(level.left != null) queue.offer(level.left);
              
                if(level.right != null)queue.offer(level.right);
            }
            res.add(temp);
            left2right = !left2right;
        }
```

vertical order\
[https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    List<int[]> res = new ArrayList<>();
    public List<List<Integer>> verticalTraversal(TreeNode root) {
        List<List<Integer>> result = new ArrayList();
        if(root == null){
            return result;
        }
        inorder(root, 0, 0);
        
        
        
        
        
        Collections.sort(res, (a, b) -> a[0] == b[0] ? a[1] == b[1] ? a[2] - b[2] : a[1] - b[1] : a[0] - b[0]);

        Map<Integer, List<Integer>> map = new TreeMap<>();
        for (int[] p : res) {
            List<Integer> temp = map.getOrDefault(p[0], new ArrayList<>());
            temp.add(p[2]);
            map.put(p[0], temp);
        }

        
        for (List<Integer> l : map.values())
            result.add(l);
        
        return result;
    }
    
    public void inorder(TreeNode root, int column, int height){
        if(root == null){
            return;
        }
        
        inorder(root.left, column - 1, height + 1);
        res.add(new int[] {column, height, root.val});
        inorder(root.right, column + 1, height + 1);
    }
}
```

