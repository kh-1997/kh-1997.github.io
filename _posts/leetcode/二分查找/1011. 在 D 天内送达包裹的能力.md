---
layout:     post
title:      "在 D 天内送达包裹的能力"
date:       2018-08-16 12:00:00
author:     "KH"
header-img: "img/post-bg-miui6.jpg"
tags:
    - 二分查找
---

# LeetCode-1011. 在 D 天内送达包裹的能力

------
#### 题目链接

中文链接(https://leetcode-cn.com/problems/capacity-to-ship-packages-within-d-days/)

#### 题目描述

传送带上的包裹必须在 D 天内从一个港口运送到另一个港口。

传送带上的第 i 个包裹的重量为 weights[i]。每一天，我们都会按给出重量的顺序往传送带上装载包裹。我们装载的重量不会超过船的最大运载重量。

返回能在 D 天内将传送带上的所有包裹送达的船的最低运载能力。

示例 1：

输入：weights = [1,2,3,4,5,6,7,8,9,10], D = 5
输出：15
解释：
船舶最低载重 15 就能够在 5 天内送达所有包裹，如下所示：
第 1 天：1, 2, 3, 4, 5
第 2 天：6, 7
第 3 天：8
第 4 天：9
第 5 天：10

请注意，货物必须按照给定的顺序装运，因此使用载重能力为 14 的船舶并将包装分成 (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) 是不允许的。 

#### 解题思路

- 在连续的空间线性搜索，这就是⼆分查找可以发挥作⽤的标志。由于我们要求的是最⼩速度，所以可以⽤⼀个搜索左侧边界的⼆分查找来代替线性搜索，提升效率。

```
class Solution {
    public int shipWithinDays(int[] weights, int D) {
        int minV = 0;
        int maxV = 0;
        for(int w:weights){
            minV = Math.max(minV,w);
            maxV += w;
        }
        int left = minV;
        int right = maxV;
        while(left<=right){
            int mid = (right-left)/2 + left;
            if(canF(mid,weights,D)){
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }
        return left;
    }

    public boolean canF(int load,int[]weights,int day){
        int i = 0;
        for(int j=0;j<day;j++){
            int loads = load;
            while(loads-weights[i]>=0){
                loads = loads - weights[i];
                i++;
                if(i==weights.length){
                    return true;
                }
            }
        }
        return false;
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