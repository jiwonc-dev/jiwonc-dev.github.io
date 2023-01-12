---
title:  "Is subTree"
excerpt: "Implement an algorithm that checks whether one tree is a subtree of the other tree."

categories:
  - algorithm

toc: true
toc_sticky: true
 
date: 2023-01-12
---

## GO code

```
package main
import "fmt"

/*
    Test Tree 1
            10
          /  \
        5     13 
      /  \   /
    3    8 11
            \
             12
             
    Test Tree 2
        5
      /  \
    3    8 
    
    Test Tree 3
        12
      /
    11    
*/

type Node struct {
	data   int
	
	// child
	left *Node
    right *Node
}

func (node *Node)setChildToLeft(child *Node) {
    node.left = child
}

func (node *Node)setChildToRight(child *Node) {
    node.right = child
}

type Tree struct {
	root *Node
}

func (tree *Tree)IsSubTree(targetTree *Tree) bool {
    targetSubRoot := findSubRoot(targetTree.root, tree.root.data)
    if targetSubRoot == nil {
        return false
    }
    return !isDifferent(targetSubRoot, tree.root)
}

func main() {
    tree1, tree2, tree3 := createTestTrees()
    fmt.Printf( "Is tree2 is subtree of tree1? %t\n", tree2.IsSubTree(tree1) )
    fmt.Printf( "Is tree3 is subtree of tree1? %t\n", tree3.IsSubTree(tree1) )
}

func createTestTrees() (*Tree,*Tree, *Tree) {
    tree1 := &Tree{}
    tree1.root = createNode(10)
    tree1.root.setChildToLeft(createNode(5))
    tree1.root.setChildToRight(createNode(13))
    tree1.root.left.setChildToLeft(createNode(3))
    tree1.root.left.setChildToRight(createNode(8))
    tree1.root.right.setChildToLeft(createNode(11))
    tree1.root.right.left.setChildToRight(createNode(12))
    
    tree2 := &Tree{}
    tree2.root = createNode(5)
    tree2.root.setChildToLeft(createNode(3))
    tree2.root.setChildToRight(createNode(8))
    
    tree3 := &Tree{}
    tree3.root = createNode(12)
    tree3.root.setChildToLeft(createNode(11))

	return tree1, tree2, tree3
}

func createNode(data int) *Node {
    return &Node{data : data}
}

func findSubRoot(root *Node, data int) *Node {
    if root == nil {
        return nil
    }
    if root.data == data {
        return root
    }
    
    var result *Node
    if root.left != nil {
        result = findSubRoot(root.left, data)
    }
    if result == nil && root.right != nil {
        result = findSubRoot(root.right, data)
    }
    return result
}

func isDifferent(a, b *Node) bool {
    if a == nil || b == nil || a.data != b.data {
        return true
    }
    
    result := false
    if a.left != nil {
        result = isDifferent(a.left, b.left)
    } else if b.left != nil {
        return true
    }
    if a.right != nil {
        result = isDifferent(a.right, b.right)
    } else if b.right != nil {
        return true
    }
    return result
}
```

## output
```
Is tree2 is subtree of tree1? true
Is tree3 is subtree of tree1? false

```

## big-O time
O(A+B)
> A : the number of nodes in the main tree   
> B : the number of nodes in the sub tree
