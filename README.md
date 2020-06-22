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
function inOrderTraversal(root, arr) {
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
function inOrderTraversal(root, arr) {
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

    if ( (min !== null && root.val <= min) || (max !== null && root.val >= max) ) return false;
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
var numTrees = function(n) {
  // simple factorial problem
  function factorial(num){
    if (num <= 0) return 1;
    else return num * factorial(num-1);
  }
  
  // catalan number formula to count total sequance of numbers
  // 2n!/(n+1)!n!
  return factorial( 2 * n ) / ( factorial( n + 1 ) * factorial( n ) );
};
```