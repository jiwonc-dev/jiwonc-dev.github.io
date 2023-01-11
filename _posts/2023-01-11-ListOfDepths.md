---
title:  "List of depths"
excerpt: "An algorithm that links nodes at the same depth to a linked list when a binary tree is given"

categories:
  - datastructure

toc: true
toc_sticky: true
 
date: 2023-01-11
---

## GO code

```
package main
import "fmt"

/*
    Test Tree 
                 A
              /    \
            B       C
          /  \     /  \
         D    E   F    G
        / \  / \ / \  / \
       H  I J  K L M  N  O
*/

type TreeNode struct {
    data string
    next *TreeNode
    
    // child
    left *TreeNode
    right *TreeNode
}

func (node *TreeNode) addNodeToLeft(child *TreeNode) {
    node.left = child
}

func (node *TreeNode) addNodeToRight(child *TreeNode) {
    node.right = child
}

type Tree struct {
    root *TreeNode
}

type LinkedList struct {
    front *TreeNode
    rear *TreeNode
}

func main() {
    tree := createTestTree()
    
    // map[depth]*LinkedList
    depthMap := getDepthSubList(tree)
    
    for i := 0; i < len(depthMap); i++ {
        subList := depthMap[i]
        if subList != nil {
            pointer := subList.front
            fmt.Printf( "depth : %d { ", i )
            startString := true
            for pointer != nil {
                str := ""
                if startString {
                    str = "%s"
                    startString = false
                } else {
                    str = ", %s"
                }
                fmt.Printf( str, pointer.data )
                pointer = pointer.next
            }
            fmt.Printf( " }\n" )
        }
    }
}

func createTestTree() *Tree {
    tree := &Tree{}
    tree.root = createNode("A")
    
    tree.root.addNodeToLeft(createNode("B"))
    tree.root.addNodeToRight(createNode("C"))
    
    left := tree.root.left
    left.addNodeToLeft(createNode("D"))
    left.addNodeToRight(createNode("E"))
    right := tree.root.right
    right.addNodeToLeft(createNode("F"))
    right.addNodeToRight(createNode("G"))
    
    subLeft := left.left
    subLeft.addNodeToLeft(createNode("H"))
    subLeft.addNodeToRight(createNode("I"))
    subRight := left.right
    subRight.addNodeToLeft(createNode("J"))
    subRight.addNodeToRight(createNode("K"))
    subLeft = right.left
    subLeft.addNodeToLeft(createNode("L"))
    subLeft.addNodeToRight(createNode("M"))
    subRight = right.right
    subRight.addNodeToLeft(createNode("N"))
    subRight.addNodeToRight(createNode("O"))
    
    return tree
}

func createNode(data string) *TreeNode {
    return &TreeNode{data : data }
}

func getDepthSubList(tree *Tree) map[int]*LinkedList {
    // map[depth]*LinkedList
    depthMap := map[int]*LinkedList{}
    setDepthNode(tree.root, 0, depthMap)
    return depthMap
}

func setDepthNode(node *TreeNode, depth int, depthMap map[int]*LinkedList) {
    if node.left != nil {
        setDepthNode(node.left, depth+1, depthMap)
    }
    if node.right != nil {
        setDepthNode(node.right, depth+1, depthMap)
    }
    if depthMap[depth] == nil {
        depthMap[depth] = &LinkedList{front : node, rear : node}
    } else {
        // enqueue
        depthMap[depth].rear.next = node
        depthMap[depth].rear = node
    }
}
```

## output
```
depth : 0 { A }
depth : 1 { B, C }
depth : 2 { D, E, F, G }
depth : 3 { H, I, J, K, L, M, N, O }
```

## big-O
- insertion : O(log n)
- print : O(n)