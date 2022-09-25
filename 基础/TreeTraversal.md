# 递归比较简单，略过。

# 循环

## 前序遍历

```java
// 前序遍历，因为是根左右、所以压栈的时候，先右后左

public void preTraversal(TreeNode root) {
	if(null == root) {
		return res;
	}
	Stack<TreeNode> stack = new Stack<>();
	stack.push(root);

	while(!stack.isEmpty()) {
	
		TreeNode node = stack.pop();
		printf(node);
	
		if(node.right != null) {
			stack.push(node.right);
		}
		if(node.left != null) {
			stack.push(node.left);
		}
  }
}
```

## 中序遍历
```java
// 中序需要先遍历到最左节点，所以需要一个cur指针。遍历到最左了，就打印自己，然后看右子树

public void inTraversal(TreeNode root) {
	if(null == root) {
		return;
	}
	Stack<TreeNode> stack = new Stack<>();
	TreeNode cur = root;
	
	while(!stack.isEmpty() || null != cur) {
	
		while(null != cur) {
			stack.push(cur);
			cur = cur.left;
		}
		TreeNode node = stack.pop();
		printf(node);
		cur = node.right;
	}
}
```

## 后序遍历

```java
// 复杂点在于，会两次经过root，第一次经过是，不能print，需要第二次经过才能print。
// 所以可以设置一个pre,如果右节点为空或者pre == 右节点，说明右节点遍历过了，可以print本节点， pre节点在某个节点被print打印后设置
public void postTraversal(TreeNode root) {
	if(null == root) {
		return;
	}
	Stack<TreeNode> stack = new Stack<>();
	TreeNode pre = null;
	TreeNode cur = root;

	while(cur != null || !stack.isEmpty()) {
	
		while(cur != null) {
			stack.push(cur);
			cur = cur.left;
		}
		cur = stack.pop();
	
		if(cur.right == null || cur.right == pre) {
			printf(cur.val);
			pre = cur;
			cur = null;  // 和前序中序不同，前序和中序，自然的会因为右节点为空，然后从stack中弹出父节点，
			 // 后序遍历中，因为最后一个节点是根节点，所以需要手动置空，然父节点弹出
	
		}  else {
			stack.push(cur);
			cur = cur.right;
		}
	}
}
```







