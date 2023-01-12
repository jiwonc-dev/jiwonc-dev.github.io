---
title:  "Lowest Common Ancestor in a Binary Tree"
excerpt: "The lowest common ancestor is the lowest node in the tree that has both n1 and n2 as descendants, where n1 and n2 are the nodes for which we wish to find the LCA(Lowest Common Ancestor). Hence, the LCA of a binary tree with nodes n1 and n2 is the shared ancestor of n1 and n2 that is located farthest from the root."

categories:
  - algorithm

toc: true
toc_sticky: true
 
date: 2023-01-12
---

## concept

[GeeksForGeeks]("https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/")

The lowest common ancestor is the lowest node in the tree that has both n1 and n2 as descendants, where n1 and n2 are the nodes for which we wish to find the LCA(Lowest Common Ancestor). Hence, the LCA of a binary tree with nodes n1 and n2 is the shared ancestor of n1 and n2 that is located farthest from the root. 


## GO code

```
package main
import "fmt"

/*
    Test Tree
            A
          /  \
        B     C 
      /  \   /
    D     E F
            \
             G

*/

type Node struct {
	data   string
	
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

func (tree *Tree)findFirstCommonAncestor(a, b string) {
    aPath := []string{}
    findNode(tree.root, a, &aPath)
    bPath := []string{}
    findNode(tree.root, b, &bPath)
    
    if len(aPath) == 0 || len(bPath) == 0 {
        fmt.Errorf( "error" )
    }
    for i := 0; i < len(aPath) && i < len(bPath); i++ {
        if aPath[i] != bPath[i] {
            fmt.Printf( "%s and %s have a first common ancestor %s\n", a, b, aPath[i-1])
            return
        }
    }
    fmt.Errorf( "error" )
}

func main() {
    tree := createTestTree()
    tree.findFirstCommonAncestor("B", "G")
    tree.findFirstCommonAncestor("D", "E")
}

func createTestTree() *Tree {
    tree := &Tree{}
    tree.root = createNode("A")
    tree.root.setChildToLeft(createNode("B"))
    tree.root.setChildToRight(createNode("C"))
    tree.root.left.setChildToLeft(createNode("D"))
    tree.root.left.setChildToRight(createNode("E"))
    tree.root.right.setChildToLeft(createNode("F"))
    tree.root.right.left.setChildToRight(createNode("G"))

	return tree
}

func createNode(data string) *Node {
    return &Node{data : data}
}

func findNode(parent *Node, data string, pathList *[]string) bool {
    if parent == nil {
        return false
    }
    *pathList = append(*pathList, parent.data)
    
    if parent.data == data {
        return true
    }
    
    if (parent.left != nil && findNode(parent.left, data, pathList)) || 
    (parent.right != nil && findNode(parent.right, data, pathList)) {
        return true
    }
    
    *pathList = (*pathList)[:len(*pathList)-1]
    return false
}
```

## output
```
B and G have a first common ancestor A
D and E have a first common ancestor B
```

## big-O time
O(N)
> The tree is traversed twice, and then path arrays are compared. 