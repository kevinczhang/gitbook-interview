# Binary Tree Preorder Traversal

## Solution

```java
// Recursive Solution
public ArrayList<Integer> preorderTraversal(TreeNode root) {
	ArrayList<Integer> re = new ArrayList<Integer>();
	if (root == null) return re;
	re.add(root.val);
	re.addAll(preorderTraversal(root.left));
	re.addAll(preorderTraversal(root.right));
	return re;
}

// Iterative Solution
public ArrayList<Integer> preorderTraversal(TreeNode root) {
	ArrayList<Integer> res = new ArrayList<Integer>();
	if(root == null) return res;
	Stack<TreeNode> stack = new Stack<TreeNode>();
	stack.push(root);
	while(!stack.isEmpty()){
		root = stack.pop();
		res.add(root.val);
		if(root.right != null) 
			stack.push(root.right);
		if(root.left != null) 
			stack.push(root.left);
	}
	return res;
}

```
