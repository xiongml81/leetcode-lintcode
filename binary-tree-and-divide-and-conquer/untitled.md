# 242. Convert Binary Tree to Linked Lists by Depth

[https://www.lintcode.com/problem/convert-binary-tree-to-linked-lists-by-depth/](https://www.lintcode.com/problem/convert-binary-tree-to-linked-lists-by-depth/)  


```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    /**
     * @param root the root of binary tree
     * @return a lists of linked list
     */
    public List<ListNode> binaryTreeToLists(TreeNode root) {

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        List<ListNode> res = new ArrayList<ListNode>();

        if(root == null) return res;

        while(!queue.isEmpty()){
            int size = queue.size();
            ListNode headNode = null;
            ListNode tailNode = null;
            for(int i = 0; i < size; i++){
                TreeNode node = queue.poll();
                if(headNode == null){
                    headNode = new ListNode(node.val);
                    tailNode = headNode;
                }
                else{
                    tailNode.next = new ListNode(node.val);
                    tailNode = tailNode.next;
                }

                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
            }
            res.add(headNode);
        }

        return res;
        
    }
}
```

