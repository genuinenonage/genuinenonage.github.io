---
title: 剑指offer算法总结
date: 2020/08/20 19:47:00
tags: 
- 算法
- offer
categories:
- 算法
---
## 03. 数组中重复的数字 
利用集合的唯一性。
	Set<Integer> set = new HashSet<Integer>();
	  
	set.add(value)  
* 集合中没有返回true
* 集合中已存在，返回false
