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

<script src="https://gist.github.com/jiwonc-dev/512c502ac027ed3cd4fde55bdb7d3edb.js"></script>

## output
```
B and G have a first common ancestor A
D and E have a first common ancestor B
```

## big-O time
O(N)
> The tree is traversed twice, and then path arrays are compared. 
