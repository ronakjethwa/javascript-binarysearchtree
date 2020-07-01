## Binary Search Tree in JavaScript

### Questions

#### InOrder Traversel

```js
function inOrderTraversal(root, arr) {
  arr = arr || [];
  if (root !== null) {
    inOrderTraversal(root.left, arr);
    arr.push(root.val);
    inOrderTraversal(root.right, arr);
  }
  return arr;
}
```

#### PostOrder Traversel

```js
function postOrderTraversal(root, arr) {
  arr = arr || [];
  if (root !== null) {
    inOrderTraversal(root.left, arr);
    inOrderTraversal(root.right, arr);
    arr.push(root.val);
  }
  return arr;
}
```

#### PreOrder Traversel

```js
function preOrderTraversal(root, arr) {
  arr = arr || [];
  if (root !== null) {
    arr.push(root.val);
    inOrderTraversal(root.left, arr);
    inOrderTraversal(root.right, arr);
  }
  return arr;
}
```

#### N-ary Tree Postorder Traversal

```js

function Node(val,children) {
    this.val = val;
    this.children = children;
};

cosnt postOrder = function(root){
    let arr = [];
    traverse(root);

    function traverse(node){
        if (!node) return;
        for (child of node.children){
            traverse(child);
        }
        arr.push(node.val);
    }

    return arr;
}
```

#### N-ary Tree Preorder Traversal

```js
function Node(val, children) {
  this.val = val;
  this.children = children;
}

var preorder = function (root) {
  const result = [];

  function traverse(node) {
    if (!node) return;
    result.push(node.val);
    for (child of node.children) {
      traverse(child);
    }
  }
  traverse(root);
  return result;
};
```

#### Validate Binary Search Tree

```js
function TreeNode(val, left, right) {
  this.val = val === undefined ? 0 : val;
  this.left = left === undefined ? null : left;
  this.right = right === undefined ? null : right;
}

var isValidBST = function (root) {
  function helper(root, min, max) {
    if (!root) return true; // We hit the end of the path

    if ((min !== null && root.val <= min) || (max !== null && root.val >= max))
      return false;
    // current node's val doesn't satisfy the BST rules

    // Continue to scan left and right
    return (
      helper(root.left, min, root.val) && helper(root.right, root.val, max)
    );
  }

  return helper(root, null, null);
};
```

#### Same Binary Tree

```js
// Definition for a binary tree node.
function TreeNode(val, left, right) {
    this.val = (val===undefined ? 0 : val)
    this.left = (left===undefined ? null : left)
    this.right = (right===undefined ? null : right)
}

const isSameTree = function(p,q){
    // if both null, return true
    if (!p && !q) return true;

    // if any of null or value is not same, return false
    if (!p || !q !! p.val !== q.val) return false;

    // keep on traversing left and right for same check
    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}
```

#### Unique Numbers Of Binary Search Trees

```js
var numTrees = function (n) {
  // simple factorial problem
  function factorial(num) {
    if (num <= 0) return 1;
    else return num * factorial(num - 1);
  }

  // catalan number formula to count total sequence of numbers
  // 2n!/(n+1)!n!
  return factorial(2 * n) / (factorial(n + 1) * factorial(n));
};
```

#### Min Value in BST

```js
function minNode(node) {
  if (!node) return 0;
  if (node.left) return minNode(node.left);
  return node.value;
}
```

#### Max Value in BST

```js
function maxNode(node) {
  if (!node) return 0;
  if (node.right) return maxNode(node.right);
  return node.value;
}
```

#### Min Height of BST

```js
var minDepth = function (root) {
  if (!root) return 0;
  let leftHeight = minDepth(root.left);
  let rightHeight = minDepth(root.right);

  return leftHeight === 0 || rightHeight === 0
    ? leftHeight + rightHeight + 1
    : Math.min(leftHeight, rightHeight) + 1;
};
```

#### Max Height of BST

```js
var maxDepth = function (root) {
  if (!root) return 0;
  let left = maxDepth(root.left);
  let right = maxDepth(root.right);

  return Math.max(left, right) + 1;
};
```

#### Convert Sorted Array to Binary Search Tree

```js
var sortedArrayToBST = function (nums) {
  if (nums.length === 0) return null;

  let mid = Math.floor(nums.length / 2);
  let root = new TreeNode(nums[mid]);

  root.left = sortedArrayToBST(nums.slice(0, mid));
  root.right = sortedArrayToBST(nums.slice(mid + 1));

  return root;
};
```

#### Lowest Common Ancestor of a Binary Tree

```js
var lowestCommonAncestor = function (root, p, q) {
  // if root reached to either of the nodes or null, return root
  if (!root || root === p || root === q) return root;

  const left = lowestCommonAncestor(root.left, p, q);
  const right = lowestCommonAncestor(root.right, p, q);

  if (!left) return right; // p and q are in the right subtree
  if (!right) return left; // p and q are in the left subtree
  return root; // p is in one side and q is in the other
};
```

#### Invert Binary Tree

```js
let invertTree = (root) => {
  if (!root) return null;
  [root.left, root.right] = [root.right, root.left]; // swap
  invertTree(root.left);
  invertTree(root.right);
  return root;
};
```

#### Flatten Binary Tree to Linked List

```js
var flatten = function (root) {
  let prev = null;
  let recurse = (root) => {
    if (!root) return;
    recurse(root.right);
    recurse(root.left);
    root.right = prev;
    root.left = null;
    prev = root;
  };
  recurse(root);
};
```

#### Find All The Lonely Nodes

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var getLonelyNodes = function (root, arr = []) {
  if (!root) return arr;

  if (!root.left && root.right) arr.push(root.right.val);
  if (root.left && !root.right) arr.push(root.left.val);

  getLonelyNodes(root.left, arr);
  getLonelyNodes(root.right, arr);

  return arr;
};
```
