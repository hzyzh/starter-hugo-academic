---
title: artificial_intelligence
date: 2022-09-19 09:33:17
tags: 
    - Lecture notes
    - CS
    - Artificial Intelligence
categories:
    - Lecture notes
math: true
---

## Ch2. 搜索

OPEN, CLOSED列表：OPEN记录待搜索结点；CLOSED记录已搜索结点

#### 最佳优先搜索

定义一个启发式算法：按照一定启发式函数 对每个OPEN结点排序；按顺序在OPEN中搜索

#### A* 算法

每个节点的优先级：$f(n)=g(n)+h(n)$

- $f(n)$，n的综合优先级；$g(n)$，n距离起点的代价（bfs）；$h(n)$，n距离终点的预计代价，**启发函数**！

- 若$h(n)$始终=0，则退化为了Dijkstra算法；
- 若$h(n)$始终<=节点n到终点的代价，则A*算法保证能找到最优路径！
