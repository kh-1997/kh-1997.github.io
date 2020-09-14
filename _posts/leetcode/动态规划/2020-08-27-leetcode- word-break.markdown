---
layout:     post
title:      "word-break"
subtitle:   "动态规划"
date:       2020-08-30 12:00:00
author:     "KH"
header-img: "img/post-bg-apple-event-2015.jpg"
tags:
    - 动态规划
    - 产品
---

> 

## 题目描述

给定一个字符串s和一组单词dict，判断s是否可以用空格分割成一个单词序列，使得单词序列中所有的单词都是dict中的单词（序列可以包含一个或多个单词）。

例如:
给定s=“leetcode”；
dict=["leet", "code"].
返回true，因为"leetcode"可以被分割成"leet code".



Given a string s and a dictionary of words dict, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

For example, given

s ="leetcode",
dict =["leet", "code"].

Return true because"leetcode"can be segmented as"leet code".

### 题目思路

初始化dp[0] = true; 定义dp[i] 代表前i个字符是否能被break；

当dp[j]==true&&dict.contains(s.substring(j,i)) dp[i] = true;

```vim
import java.util.*;
public class Solution {
    public boolean wordBreak(String s, Set<String> dict) {
        
        if(s==null||s.length()==0) return false;
        boolean[] dp = new boolean[s.length()+1];
        dp[0] = true;
        for(int i=1;i<=s.length();i++){
            for(int j=0;j<i;j++){
                if(dp[j]&&dict.contains(s.substring(j,i))){
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```





