# Binary Tree Postorder Traversal

## Solution

```java
// Recursive Solution
public ArrayList<Integer> postorderTraversal(TreeNode root) {
	ArrayList<Integer> re = new ArrayList<Integer>();
	if (root == null) return re;
	re.addAll(postorderTraversal(root.left));
	re.addAll(postorderTraversal(root.right));
	re.add(root.val);
	return re;
}

// Iterative Solution
public ArrayList<Integer> postorderTraversal(TreeNode root) {
	ArrayList<Integer> res = new ArrayList<Integer>();
	if (root == null) return res;
	Stack<TreeNode> parentStack = new Stack<TreeNode>();
	TreeNode lastnodevisited = root, peekNode;
	while (!parentStack.isEmpty() || root != null) {
		if (root!= null) {
			parentStack.push(root);
			root = root.left;
		} else {
			peekNode = parentStack.peek();
			// If right child exists AND traversing node from left child, move right
			if (peekNode.right != null && lastnodevisited != peekNode.right) {
				root = peekNode.right;
			} else {
				parentStack.pop();
				res.add(peekNode.val);
				lastnodevisited = peekNode;
			}
		}
	}
	return res;

}
```
