---
layout:     post
title:      "bfs"
date:       2018-08-16 12:00:00
author:     "KH"
header-img: "img/post-bg-miui6.jpg"
tags:
    - bfs
---

# LeetCode-111. 二叉树的最小深度

------
#### 题目链接

中文链接(https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

#### 题目描述

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

说明: 叶子节点是指没有子节点的节点。

示例:

给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
​    /  \
   15   7
返回它的最小深度  2.

#### 解题思路

- bfs

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int minDepth(TreeNode root) {
        if(root==null) return 0;
        Queue<TreeNode>queue = new LinkedList<>();
        queue.add(root);
        int step = 1;
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i=0;i<size;i++){
                TreeNode cur = queue.poll();
                if(cur.left==null&&cur.right==null){
                    return step;
                }
                if(cur.left!=null){
                    queue.add(cur.left);
                }
                if(cur.right!=null){
                    queue.add(cur.right);
                }

            }
            step++;
        }
        return step;
    }
}
```



# LeetCode-752. 打开转盘锁

------
#### 题目链接

中文链接(https://leetcode-cn.com/problems/open-the-lock/)

#### 题目描述

你有一个带有四个圆形拨轮的转盘锁。每个拨轮都有10个数字： '0', '1', '2', '3', '4', '5', '6', '7', '8', '9' 。每个拨轮可以自由旋转：例如把 '9' 变为  '0'，'0' 变为 '9' 。每次旋转都只能旋转一个拨轮的一位数字。

锁的初始数字为 '0000' ，一个代表四个拨轮的数字的字符串。

列表 deadends 包含了一组死亡数字，一旦拨轮的数字和列表里的任何一个元素相同，这个锁将会被永久锁定，无法再被旋转。

字符串 target 代表可以解锁的数字，你需要给出最小的旋转次数，如果无论如何不能解锁，返回 -1。

示例 1:

输入：deadends = ["0201","0101","0102","1212","2002"], target = "0202"
输出：6
解释：
可能的移动序列为 "0000" -> "1000" -> "1100" -> "1200" -> "1201" -> "1202" -> "0202"。
注意 "0000" -> "0001" -> "0002" -> "0102" -> "0202" 这样的序列是不能解锁的，
因为当拨动到 "0102" 时这个锁就会被锁定。

#### 解题思路

- bfs

```
class Solution {
    public int openLock(String[] deadends, String target) {
        Queue<String>queue = new LinkedList<>();
        HashSet<String>list = new HashSet<>();
        HashSet<String>dead = new HashSet<>();
        for(String s:deadends){
            dead.add(s);
        }
        queue.offer("0000");
        list.add("0000");
        int step = 0;
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i=0;i<size;i++){
                String tmp = queue.poll();
                if(tmp.equals(target)){
                    return step;
                }
                if(dead.contains(tmp)){
                    continue;
                }
                for(int k=3;k>=0;k--){
                    String up = plusOne(tmp,k);
                    if(!list.contains(up)){
                         queue.add(up);
                         list.add(up);
                    }
                    String down = minusOne(tmp,k);
                    if(!list.contains(down)){
                         queue.add(down);
                         list.add(down);
                    }
                }
            }
            step++;
        }
        return -1;
    }

    public String plusOne(String s,int j){
        char[] ch = s.toCharArray();
        if(ch[j]=='9'){
            ch[j] = '0';
        }else{
            ch[j] += 1;
        }
        return new String(ch);
    }

    public String minusOne(String s,int j){
        char[] ch = s.toCharArray();
        if(ch[j] == '0'){
            ch[j] = '9';
        }else{
            ch[j] -= 1;
        }
        return new String(ch);
    }

}
```

作者 [@kh-1997][3]     
2020 年 08月08日    