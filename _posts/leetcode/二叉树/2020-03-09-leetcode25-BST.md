---
layout: post
title: '二叉搜索树转换链表'
subtitle: '二叉搜索树'
date: 2020-03-08
categories: program
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: leetcode﻿
---

# LeetCode

------

# 二叉搜索树

#### 题目描述

1、给定一个单链表，其中的元素按升序排序，请将它转化成平衡二叉搜索树（BST）

2、给出一个升序排序的数组，将其转化为平衡二叉搜索树（BST）.

#### 解题思路

思路：这道题是要求把有序链表转为二叉搜索树，和之前那道Convert Sorted Array to Binary Search Tree思路完全一样，只不过是操作的数据类型有所差别，一个是数组，一个是链表。数组方便就方便在可以通过index直接访问任意一个元素，而链表不行。由于二分查找法每次需要找到中点，而链表的查找中间点可以通过快慢指针来操作。找到中点后，要以中点的值建立一个数的根节点，然后需要把原链表断开，分为前后两个链表，都不能包含原中节点，然后再分别对这两个链表递归调用原函数，分别连上左右子节点即可。

#### 实现代码

```
public TreeNode sortedListToBST(ListNode head) {
        return toBST(head, null);
    }
 
    private TreeNode toBST(ListNode head, ListNode tail) {
        if (head == tail)
            return null;
        // 申请两个指针，fast移动速度是low的两倍
        ListNode fast = head;
        ListNode slow = head;
        while (fast != tail && fast.next != tail) {
            fast = fast.next.next;
            slow = slow.next;
        }
        TreeNode root = new TreeNode(slow.val);
        root.left = toBST(head, slow);
        root.right = toBST(slow.next, tail);
 
        return root;
    }

```

```
这道题是二分查找树的题目，要把一个有序数组转换成一颗二分查找树。
 ``* 从本质来看，如果把一个数组看成一棵树（也就是以中点为根，左右为左右子树，依次下去）
 ``* 数组就等价于一个二分查找树。
 ``* 所以如果要构造这棵树，那就是把中间元素转化为根，然后递归构造左右子树。
 ``* 所以我们还是用二叉树递归的方法来实现，以根作为返回值，每层递归函数取中间元素，
 ``* 作为当前根和赋上结点值，然后左右结点接上左右区间的递归函数返回值。
 ``* \时间复杂度还是一次树遍历O(n)，
 ``* 总的空间复杂度是栈空间O(logn)加上结果的空间O(n)，额外空间是O(logn)，总体是O(n)。
```

```
链接：https://www.nowcoder.com/questionTerminal/7e5b00f94b254da599a9472fe5ab283d?f=discussion
来源：牛客网

public class Solution {
    public TreeNode sortedArrayToBST(int[] num) {
        if(num.length==0)
            return null;
        int start=0;
        int end=num.length;
        //注意边界问题 
        //end取不到
        return toBST(num,start,end);
    }
    private TreeNode toBST(int[] num,int start,int end){
        if(start==end)
            return null;
        int mid =(start+end)/2;
        TreeNode root =new TreeNode(num[mid]);
        root.left=toBST(num,start,mid);
        root.right=toBST(num,mid+1,end);
        return root;
    }
}
```



作者 [@kh-1997][3]     
2020 年 03月08日    