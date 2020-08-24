---
layout: post
title: "求给定二叉树的最小深度"
subtitle: 'From Vim to Spacemacs'
author: "kh"
header-style: text
tags:
  - 刷题
---

Emacs tend to provide a good support for functional programming languages. Indeed, many FP language community exclusively use Emacs and give only first-party IDE supports to Emacs, such as Coq, Agda, Standard ML, Clojure, etc.




### 题目描述

求给定二叉树的最小深度。最小深度是指树的根结点到最近叶子结点的最短路径上结点的数量。

Given a binary tree, find its minimum depth.The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.


### 题目思路

It's there! 二叉树前序遍历

```vim
import java.util.*;

/*
 * public class TreeNode {
 *   int val = 0;
 *   TreeNode left = null;
 *   TreeNode right = null;
 * }
 */

public class Solution {
    /**
     * 
     * @param root TreeNode类 
     * @return int整型
     */
    public int run (TreeNode root) {
        // write code here
        if(root==null) return 0;
        if(root.left==null&&root.right==null){
            return 1;
        }
        int left = run(root.left);
        int right = run(root.right);
        if(left==0||right==0){
            return left+right+1;
        }
        return left<right?left+1:right+1;
        
    }
}
```











