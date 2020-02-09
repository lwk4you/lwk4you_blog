---
title: 每日leetCode之两数之和
date: 2019-12-14 21:13:50
tags: [leetCode,两数之和,twoSum,easy]
categories: [学习, leetCode]
mathjax: true
---
对于一个想要提升自身编程水平的程序员来说，leetCode是一个非常重要的题库。涉及的算法题不仅能让你应付面试中必考的算法题，也对自己代码的质量和算法优缺点有比较明显
的了解。

所以现在会定期刷算法题，当然估计不会像学生党天天刷。作为一个半路出家的java工程师，会保证定期定量的刷，习惯和坚持才是最好的老师。

目前主要用的是leetCode的vsCode插件，非常好用，节点用的是国内的，可以测试提交查看结果，关联自己的leetCode非常方便。

我会优先记录自己思考这道题的思路，有必要会看官网其他的思路，一起进步。

<!--more-->

## 题目内容
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

### 示例:
```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

## 题解
### 1、暴力遍历法
两数相加结果为定值
第一反应必然就是遍历相加，筛选满足条件的target返回，我确实也是这么做的，代码非常简单：
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] twoSum=new int[2];
        for(int i=0;i<nums.length-1;i++){
            for(int j=i+1;j<nums.length;j++){
                int sum=nums[i]+nums[j];
                if(sum==target){
                    twoSum[0]=i;
                    twoSum[1]=j;
                }

            }
        }
        return twoSum;       
    }
}
```
提交leetCode结果返回如下：
```
Accepted
29/29 cases passed (59 ms)

Your runtime beats 10.57 % of java submissions

Your memory usage beats 67.17 % of java submissions (38.4 MB)
```

#### 复杂度分析：

时间复杂度：$O(n^2)$
对于每个元素，我们试图通过遍历数组的其余部分来寻找它所对应的目标元素，这将耗费 $O(n)O(n)$ 的时间。因此时间复杂度为 $O(n^2)$。

空间复杂度：$O(1)$。


虽然代码正确，但速度却用了59ms，所以我们需要思考其他的思路。

### 2、构造HashMap查询法
暴力法的时间复杂度$O(n^2)$，我们期望构造$O(n)$复杂度的解决方案，在java中正好有这么一种数据结构满足要求，那就是hashmap。

#### 代码：
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }
            map.put(nums[i], i);
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```
提交leetCode结果返回如下：
```
29/29 cases passed (3 ms)
Your runtime beats 98.08 % of java submissions
Your memory usage beats 92.44 % of java submissions (37 MB)
```
#### 复杂度分析：

时间复杂度：$O(n)$，
我们把包含有 $n$ 个元素的列表遍历两次。由于哈希表将查找时间缩短到 $O(1)$ ，所以时间复杂度为 $O(n)$。

空间复杂度：$O(n)$，
所需的额外空间取决于哈希表中存储的元素数量，该表中存储了 $n$ 个元素。

这样的结果无疑是快速的，官方题解作为过渡，将两遍hash 和一遍hash做了区分，这里不做赘述。


