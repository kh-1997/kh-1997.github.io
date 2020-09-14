---
layout:     post
title:      "加起来和等于T的所有组合"
subtitle:   "回溯"
date:       2020-08-28 12:00:00
author:     "KH"
header-img: "img/post-bg-apple-event-2015.jpg"
tags:
    - 回溯
    - 产品
---

> 

## 题目描述

给出一组候选数C和一个目标数T，找出候选数中加起来和等于T的所有组合。

C中的数字在组合中可以被无限次使用

注意：

- 题目中所有的数字（包括目标数T）都是正整数
- 你给出的组合中的数字 (a 1, a 2, … , a k) 要按非递减排序 (ie, a 1 ≤ a 2 ≤ … ≤ a k).
- 结解集中不能包含重复的组合



例如：给定的候选数集是[2,3,6,7]，目标数是7

解集是：

[7][2, 2, 3]

### 题目思路

利用回溯，先对数组进行排序，然后每一层的选择，只能从小到大，选了大的就不能回过头来选小的，所以需要一个start，每次i从 start 开始选择,选择一个数，然后进入下一层即可，因为可以重复选择，所以下一层是从i开始，start=i。

```vim
 public class Solution {
    
    ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
    public ArrayList<ArrayList<Integer>> combinationSum(int[] candidates, int target) {
        if(candidates.length==0) return res;
        Arrays.sort(candidates);
        ArrayList<Integer> list = new ArrayList<Integer>();
        dfs(candidates,target,list,0);
        return res;
    }
    
    public void dfs(int[] num,int target,ArrayList<Integer> list,int start){
        if(target==0){
            ArrayList<Integer> tmp = new ArrayList<Integer>(list);
            res.add(tmp);
            return;
        }
        if(target<0){
            return;
        }
        for(int i=start;i<num.length;i++){
            list.add(num[i]);
            dfs(num,target-num[i],list,i);
            list.remove(list.size()-1);
        }
    }
}
```





