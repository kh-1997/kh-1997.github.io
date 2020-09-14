---
layout:     post
title:      "找出所有的根节点到叶子节点的节点值之和等于的路径"
subtitle:   "回溯解法"
date:       2020-08-27 12:00:00
author:     "KH"
header-img: "img/post-bg-apple-event-2015.jpg"
tags:
    - 二叉树
    - 产品
---

> 这篇文章转载牛客网

### 题目描述

给定一个二叉树和一个值\ sum sum，请找出所有的根节点到叶子节点的节点值之和等于\ sum sum 的路径，
例如：
给出如下的二叉树，\ sum=22 sum=22，

![img](https://uploadfiles.nowcoder.com/images/20200807/999991351_1596785952017_5396804DA19E4F091E6360FD4BD0F4A5)

返回
[
[5,4,11,2],
[5,8,9]
]

### 题目思路

利用回溯法解题即可。

当root==null return;

当root.left==null&&root,right==null &&sum==0   记录改路径，

否则 添加节点 进入左子节点查找，进入右子节点查找，删除节点

```vim
public class Solution {
    /**
     * 
     * @param root TreeNode类 
     * @param sum int整型 
     * @return int整型ArrayList<ArrayList<>>
     */
    ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
    public ArrayList<ArrayList<Integer>> pathSum (TreeNode root, int sum) {
        // write code here
        if(root==null) return res;
        ArrayList<Integer> list = new ArrayList<Integer>();
        dfs(root,sum,list);
        return res;
    }
    public void dfs(TreeNode root,int sum,ArrayList<Integer>list){
        if(root==null) return;
        sum-=root.val;
        list.add(root.val);
        if(sum==0&&root.left==null&&root.right==null) {
            res.add(new ArrayList<Integer>(list));
        }
        dfs(root.left,sum,list);
        dfs(root.right,sum,list);
        list.remove(list.size()-1);
    }
}
```







