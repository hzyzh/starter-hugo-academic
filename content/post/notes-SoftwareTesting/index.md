---
title: Software Testing
date: 2022-09-27 10:02:26
tags:
    - Lecture notes
    - CS
    - Software Testing
categories:
    - Lecture notes
math: true

---



## Ch. 2 白盒测试 vs 黑盒测试

#### 白盒测试

允许测试人员利用程序**内部的逻辑结构**设计测试用例，对程序所有逻辑路径进行测试。

测试对象基于被测试程序的**源代码**

##### 白盒测试方法必须遵循以下原则

- 保证一个模块中的**所有独立路径至少被测试一次**。
- 对所有的逻辑判定均需测试**取真和取假**两种情况。
- 在上下边界及可操作范围内运行所有循环。
- 检查程序的内部数据结构，保证其结构的有效性

##### 白盒测试类别

- 静态测试： 不要求在计算机上实际执行所测试的程序，主要以一些人工的模拟技术对软件进行分析和测试，如代码检查法、静态结构分析法等；

- 动态测试： 是通过输入一组预先按照一定的测试准则构造实际数据来动态运行程序，达到发现程序错误的过程。白盒测试中的动态分析技术主要有逻辑覆盖法和基本路径测试法。

##### 代码结构覆盖

<img src="..\figs\fig94.png" style="zoom: 50%;" />

- 修改决策条件覆盖？

#### 黑盒测试

完全不考虑程序的内部结构和处理过程的前提下，只基于**规格说明**来设计测试用例；又称为**功能测试**

##### 等价类划分 & 边界值分析

等价类划分：如所有符合要求的输入一类；针对违反不同规则的输入 各一类

##### Category Partition

一个程序有许多相关属性（attribute），如程序运行的：parameters，environment objects等（根据规格说明，将程序分解为若干功能单元**functional unit**）；

针对每个attribute，分出若干个categories（如对于字符串长度，分为0，1，若干，超长。。。等）；

generate test cases

##### 因果图和决策表

**等价类划分和边界值分析**都只孤立地考虑各个输入数据，而没有考虑多个输入数据间的组合效应，可能会遗漏了输入数据易于出错的组合情况

因果图可以转化为决策表，表中每一列展示了原因和结果之间的关系。可以基于决策表设计对应的测试用例（例如，为表中的每一列设计一条测试用例）

如：因果图<img src="..\figs\fig96.png" style="zoom:50%;" />，

对应决策表<img src="..\figs\fig95.png" style="zoom: 50%;" />

## Ch. 3 软件开发中的测试方法

#### 单元测试 Unit testing

 与系统一个单一功能（logical purpose）有关的代码称为一个unit；

编写一小段代码 => 测试一个很小、很明确的功能正确

**快速执行**

**自动化**

- 使用单元测试的自动化框架来自动执行单元测试用例：JUnit，NUnit，TestNG。。。
- 会自动设置测试环境、前置条件；自动执行测试用例；对比输出

#### 集成测试 Integration Testing

在单元测试的基础上，采用适当的策略将已通过测试的模块组装成子系统或系统，并确保各模块组合到一起后能按既定的设计要求运行

##### 基于分解的集成（Decomposition-based）

- 自底向上（先开发底层模块）：先从原子模块开始，逐步向上组装和测试；需要 **测试驱动程序（driver）**来调用和协调各原子模块
- 自顶向下（先开发主控制模块）：则需要 **桩程序（stub）**和 **模拟程序（mock）**
- 混合策略（sandwich）：中上层自顶向下；中下层自底向上；灵活

**基于功能集成**：每次集成提供一个用户可感知的具体功能

#### 系统测试 System Testing

将整个软件系统视为一个整体来进行测试

#### 冒烟测试 Smoke Test

在每日构建完成后，对系统的基本功能进行简单的测试，是将代码更改签入到代码库之前的验证过程

daily build（从头到尾编译、链接、运行一次） + smoke test （简单的测试）

#### 回归测试 Regression Testing

代码修改后，重新进行测试以确认修改的正确性，以及修改没有引入新的错误

- 回归测试通常要求自动化，以此来降低软件开发和维护成本
- 软件开发的各个阶段都会进行多次回归测试，新版本的连续发布会使回归测试进行的更加频繁（通常每天都需要进行若干次回归测试）
- 回归测试会对已有的测试用例库进行增删或改进

#### Flaky Test

在相同代码版本上，多次执行同一个测试用例却观察到不同的测试结果(可能因为测试用例引入了一些随机性？)
##### Flakiness 的来源 (及解决方案)

- 并发和同步相关的问题 (e.g., test makes an asynchronous call and
  does not wait, multiple threads interact, ...)
- 多条测试用例执行时的顺序和依赖问题 (e.g., shared variables, no
  cleaning up, ...)
- 数据和资源的管理与控制问题 (e.g., database connections, memory
  allocations, unordered collections, ...)
- 测试执行时间过⻓或难于控制、依赖于当前系统时间 (e.g., network, ...)
- 随机性 (e.g., random numbers generator, ...）

#### Alpha 测试

在开发环境或模拟的实际操作环境下进行的测试（通常依赖第三方测试机构）

#### Beta 测试

由软件用户在实际使用环境下进行的测试 (开发者无法控制测试环境)

##### Perpetual Beta

软件系统长期处于Beta测试中

## Ch4. 软件特性和方面的测试方法

#### 针对软件效率的测试

对于一些大规模的复杂软件系统 (Ultra Large-Scale Software Systems)，针对软件运行效率的测试非常重要

- 负载测试 Load Testing：检测系统在不同负载（concurrent users？）下的表现
  - 评估系统在不同工作量下的行为；有些问题可能需要在高负载下显现（memory leak，deadlock等）
- 压力测试 Stress Testing：检测系统在极限情况下的表现
  - 通过模拟负载，使系统在负载饱和或资源匮乏的状态下运行
  - 软件老化 (Aging) 缺陷：软件系统⻓时间运行中出现的可用资源不足、性能下降、失效率增加等现象 (⻓时间运行后性能下降)，通常是由于系统状态中的错误累计和系统资源 (例如，物理内存、文件等) 的消耗造成的
    - 通过⻓时间提供大量工作负载(例如，大量客户端请求) 使软件老化现象更快暴露出来
- 容量测试 Volume：检测系统在大数据量或大量用户下的表现
  - 通常只关注大容量，不关注实际使用
- 性能测试 Performance：评估系统的性能指标
  - 评估一堆性能指标

- 前仨**面向缺陷**；性能测试则**面向指标**

#### 可靠性测试

Reliability Testing：评估软件的可靠性程度；

软件可靠性是指软件在规定的时间和规定的环境下，完成规定功能的能力

**看看ppt！**

#### 安全性测试

检测软件安全控制机制的正确性和有效性

- 安全功能测试：测试软件实现是否与安全需求说明一致
- 安全漏洞测试：

##### 安全性测试中的常用方法

- 静态分析
  - 针对特定的攻击方式进行检查，尽早发现错误
  - 存在误报和漏报现象，需要在两者之间进行平衡
- 形式化方法 (e.g., Model Checking)
  - 具有完备的数学基础，能对形式化的规格说明进行正确性证明
  - 开发成本高，状态爆炸问题

- 模糊测试 Fuzzing
- 语法测试 Syntax Testing

#### 用户认证+授权测试

（见ppt）

#### 兼容性测试

检测软件能否在不同的**硬件平台**、**操作系统**和**网络环境**之上、以及不同的应用之间正常运行

#### 配置测试

Configuration Testing：检测软件在不同构建和运行配置下是否能正常工作

- 高可配置软件：允许用户定义一系列配置选项而保持核心功能不变
- 可能存在解空间爆炸的问题（一堆可选配置的组合）<img src="..\figs\fig97.png" style="zoom:50%;" />

#### 图形用户界面测试GUI

（每个用户操作 可能出发不同event）

基于模型的测试：定义coverage概念

- Event Flow Graph（EFG）：每个点代表event，边代表一个用户操作
  - cover nodes and edges；sequences of events
- Finite State Machine（FSM）：node代表一个界面/窗口？edge代表一个event



软件测试坐标系：<img src="..\figs\fig98.jpg" style="zoom: 25%;" />

## Ch5. Random Testing

problem：测试空间太大，无法全测

<img src="..\figs\fig99.png" style="zoom: 67%;" />

issues in RT：

- number好randomly sample，但复杂数据结构如何随机sample？（还有内存、时间限制）

RT sample的质量：diversity！

#### Adaptive Random Testing (ART)

Select test cases that are **as diverse as possible**: 

- 可以尝试 maximize distance between tests

几种implementations：

- Fixed-Size-Candidate-Set (FSCS)<img src="..\figs\fig100.png" style="zoom:67%;" />

- Partition based-ART<img src="..\figs\fig101.png" style="zoom:67%;" />

##### evaluate the distribution of a given test set:

- distribution metric

  - discrepency:<img src="..\figs\fig102.png" style="zoom:67%;" />

  - dispersion:<img src="..\figs\fig103.png" style="zoom:67%;" />

  - diversity:<img src="..\figs\fig104.png" style="zoom:67%;" />

##### ART Weaknesses: 

- 计算复杂度
- Boundary effect：更容易找到一堆边界处的test（实际不需要这么多）
- 高维效果差

### Combinatorial Testing

全部测试开销过高；且并非所有的输入参数都与fault有关 => 把fixed number t个不同参数的任意种组合情况都测试了，**t就叫该测试的coverage strength**

一个例子：<img src="..\figs\fig107.png" style="zoom:50%;" />

CT测试步骤<img src="..\figs\fig105.png" style="zoom:67%;" />

如何depict input space很关键！

（如要测试find命令）：<img src="..\figs\fig106.png" style="zoom:55%;" />

##### CT的优点

- t-way CT覆盖了小于等于t个参数的所有种interaction （exhaustive）；比穷举少多了
  - 不过随着t增大，covering array大小显著提升！
- 研究证明：绝大部分fault的产生所需interaction很少

##### Covering Array

不同参数可能有不同的value domains => Mixed Covering Array

Sequence Covering Array：

- 用于测试event顺序带来的影响，如：<img src="..\figs\fig108.png" style="zoom:55%;" />

##### 构造 t-way covering array

构造minimal t-way CA是一个NP Hard的问题！一些简化方法：

- mathematical approach
  - orthogonal array (OA)<img src="..\figs\fig109.png" style="zoom:50%;" />
  - 得到最优的CA，但limited for certain problem instances
- greedy approach
  - In-Parameter-Order (IPO) algorithm<img src="..\figs\fig110.png" style="zoom:50%;" />
  - 运行效率高，但结果不一定最优
- search-based approach
  - 得到尽可能small的array，但高计算开销

##### CT的一些constraints

- hard constraint：并非所有parameter组合都有效（有些parameter不能同时出现）

- soft constraint：测试者认为某些parameter组合没有必要测试

得到t-way constrained covering array，要求：

- CA中每一行都满足约束；任意t个参数之间 满足约束 的组合至少出现一次
  - 会引入隐性约束问题：如有约束：(P1=0,P2=0),(P2=1,P3=1) => (P1=0,P3=1)

constraint solver：用来检测一个（partial）test case是否valid

- 将所有constraints表达式用solver支持的形式表示：如boolean formula
- SAT/SMT



## FSM Testing

model-based testing：建模，将原系统 map 为一个model；是一种reduction，model仅反应系统的部分性质

根据model生成一些abstract test cases => executable test cases

- strongly connected：可以从FSM的任意状态s1转移到任意状态s2

一般假设：FSM M是minimal，strongly connected，**completely specified**；并且存在正确的reset操作（状态回到初始s）

testing FSM：根据归约（原system）检测FSM，错误包括两种：**output fault**，**state transfer fault**

#### Finding state transfer fault

确定当前state很重要（只能靠FSM的outputs判断）

##### Distinguishing sequence

<img src="..\figs\fig111.png" style="zoom:55%;" />



Distinguishing sequence是general的，还有Unique Input/Output (UIO) sequence for a state s（即所有其他状态s‘得到的输出与s的不同即可）

##### Characterizing set

<img src="..\figs\fig112.png" style="zoom: 50%;" />



一般方法：<img src="..\figs\fig113.png" style="zoom:55%;" />

##### Chow's Method (W-method)

1. 找到FSM的一个特征集W，及FSM的state cover set V（即input sequences的集合，使得从s0开始可以分别到达所有状态s）
2. 假设state数存在上限？
3. <img src="..\figs\fig114.png" style="zoom:50%;" />
   - ·表示笛卡尔积；V·W表示到达任意某个状态s（V），然后确定当前确实在状态s（W）；V·X·W表示 从s经过任意某个state transfer（V·X），然后确定确实在正确的转移状态s‘（W）

## Constraint Based Testing

针对控制流来设计sample<img src="..\figs\fig115.png" style="zoom:50%;" />

SAT： satisfying assignment （to Boolean Satisfiability）

SMT： SAT的推广，给变量赋值

#### Symbolic Execution

用symbolic values来表示 变量 和path conditions

<img src="..\figs\fig116.png" style="zoom:50%;" />

根据不同控制流对应的constraints， solve出符合的inputs => 相当于inputs的**等价类划分**

<img src="..\figs\fig117.png" style="zoom:50%;" />

一些practical issues：

- Loops，recursion，path explosion => paths过多
- 可能调用了外部库（无源码）；或约束条件过于复杂

#### Dynamic Symbolic Execution （Concolic Testing）

symbolic execution dynamically + a concrete input（简化约束求解）

<img src="..\figs\fig118.png" style="zoom:50%;" />

- 需要通过实际execute来确定当前的input对应的path condition（而不只是静态求解）
- 有了当前path condition，下一步 变换path condition中的最后一项，得到待求解的约束
- 需要通过symbolic求解器 来变换当前input => 符合待求解约束的input，再继续实际执行（第一步）

issues：

- 如何求解 待求解的约束，得到新input？一些些缓解办法：将难解/不能解的约束，用具体值替换，去求解另一边（能力有限）

  

## Search Based Software Testing

<img src="..\figs\fig119.png" style="zoom:50%;" />

在解空间中，对一个已有solution进行微调，并比较新solution，保留better one；重复该流程

（search是）heuristic的，针对一个**optimization problem**，找到一个足够好的解

#### Key Ingredients

##### Representations

##### Operators

A function that evaluates the goodness of a candidate solution

- Fitness Landscape: fitness function的hyper surface表示

Local search

- 如Hill Climbing算法；（每次考虑周围一部分的 solutions）
- 容易陷入局部最优local optima

Global search

- Simulated Annealing：灭火算法
  - 温度不断降低；温度高时，解不稳定，且易采取随机运动；温度低后，随机性降低，解趋向于稳定
- Genetic Algorithm：
  - 引入selection pressure（即根据fitness functions度量），趋向于选择更优的solutions作parents
  - <img src="..\figs\fig120.png" style="zoom:50%;" />

##### Fitness Functions

- Approach Level: 偏离的控制流节点数（但没办法guide the test）
- Branch Distance:表示当前branch 当前输入状态 距离目标predicate之间的距离  $\in[0,1)$

fitness function: $f(s,i) = approach\; level + normalised(brach\; distance)$

##### Exploitation vs. Exploration

Exploitation: 找到当前局部最优的能力

Exploration: 全局搜索的能力

之间有一个tradeoff

##### Test Suite Minimization



## Mutation Testing

