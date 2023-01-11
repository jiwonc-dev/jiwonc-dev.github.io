---
title:  "Implement balanced binary search tree"
excerpt: "implemented a binary search tree with minimum height using data in ascending arrays that are integers and have no duplicate values."

categories:
  - algorithm
tags:
  - [Algorithm]

toc: true
toc_sticky: true
 
date: 2023-01-10
---

## GO code

```

package main
import "fmt"

type TreeNode struct {
    data int
    height int
    
    // child
    left *TreeNode
    right *TreeNode
}

func (node *TreeNode) getHeight() int {
    if node == nil {
        return -1
    }
    return node.height
}

func (node *TreeNode)updateHeight() {
    node.height = max(node.left.getHeight(), node.right.getHeight()) + 1
}

type Tree struct {
    root *TreeNode
}

func (tree *Tree)Insert(data int) {
    tree.root = insertNode(tree.root, data)
}

func (tree *Tree)Traverse() {
    traverse(tree.root)
}

func insertNode(node *TreeNode, data int) *TreeNode {
    if node == nil {
        node = &TreeNode{data : data, height : 1 }
        return node
    } else if node.data < data {
        // repeat until find the leef node
        node.right = insertNode(node.right, data)
    }
    node.updateHeight()
    return balanceNode(node, data)
}

func balanceNode(node *TreeNode, data int) *TreeNode {
    bF := getBalanceFactor(node)
    
    if bF < -1 && node.right.data < data {
        node = rotateRR(node)
    }
    return node
}

func rotateRR(node *TreeNode) *TreeNode {
    newRoot := node.right
    node.right = newRoot.left
    newRoot.left = node
    
    newRoot.updateHeight()
    node.updateHeight()
    return newRoot
}

func getBalanceFactor(node *TreeNode) int {
    if node == nil {
        return 0
    }
    return node.left.getHeight() - node.right.getHeight()
}

// in-order
func traverse(node *TreeNode) {
    if node == nil {
        return
    }

    traverse(node.left)
    fmt.Println(node.data)
    traverse(node.right)
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func main() {
    ascendingIntMap := map[int]int{ 0: 1, 1: 2, 2: 5, 3: 7, 4: 9, 5:10, 6:11, 7: 14, 8 :20 }
    myAVL := &Tree{}
    for i := 0; i < len(ascendingIntMap); i++ {
        myAVL.Insert(ascendingIntMap[i])
    }
    myAVL.Traverse()
}