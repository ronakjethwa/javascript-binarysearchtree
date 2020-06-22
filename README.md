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
