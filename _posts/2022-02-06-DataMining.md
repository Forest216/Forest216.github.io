---
layout:     post                    # 使用的布局（不需要改）
title:      DataMining               # 标题 
subtitle:   数据挖掘 #副标题
date:       2022-02-06              # 时间
author:     Fu Xiaohang                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - 数据挖掘
    - 大数据
---


&emsp;&emsp;数据挖掘是从数据集中挖掘有价值的信息，数据采集仅仅是数据挖掘的第一步，后面还要进行数据清理和预处理，以及下面各项算法的挖掘等等。

# 1 数据仓库

## 1.1 与数据库的对比

&emsp;&emsp;数据库主要侧重于日常事务的处理，如银行的交易，账号的登录等等，主要应用OLTP(联机**事务**处理)；而数据仓库侧重于对大量历史数据进行分析做出决策，主要应用OLAP(联机**分析**处理)。数据仓库的数据来源于多个数据源，只进行最开始的一次数据装载，后面进行的就是大量的查询操作了。以图书表格系统举例子，如果用数据库存储的话，其表单设计如下，

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211208201042979.png" alt="image-20211208201042979" style="zoom: 50%;" />

因为数据仓库要进行大量的查询操作，而如果像数据库这样分为多个表单，要进行大量的耗时的join操作，效率不高，因此数据仓库将表合为一个，能够进行快速的复杂的查询分析，不过会有冗余数据。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211208202034167.png" alt="image-20211208202034167" style="zoom:50%;" />

数据仓库也不用像数据库那样考虑事务处理、恢复和并发控制等等。数据仓库是面向主题的，围绕一些主题进行数据集成和分析，如销售分析等等。**数据集市**是数据仓库的子集，数据仓库通常面向企业级宏观主题，数据集市则面向特定微观主题。

## 1.2 维表和事实表

- 事实表：存储能体现实际数据的值/要关注的内容，如销售量等等
- 维表：存储具有独立属性或层次结构的信息，常是一些描述性的信息，观察事物的角度，如时间、地点、类别等等，从时间来看销售量，从地区来看销售量

## 1.3 多维数据模型

### 1.3.1 数据立方体

&emsp;&emsp;当数据为三维时，其结构如下(数据值为销量)，三个维度相当于xyz轴，如季度为Q2、城市为温哥华、类型为计算的销量是952。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211208210429566.png" alt="image-20211208210429566" style="zoom:50%;" />

当数据为4维时，就可以有多个立方体，每一个立方体代表维度supplier为一个值时的情况。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211208211010961.png" alt="image-20211208211010961" style="zoom: 67%;" />

OLAP操作：

- 上卷(roll-up)：向上汇总数据，如街道→城市→省→国家
- 下钻(drill-down)：向下细分数据，如年→季度→月→日
- 切片(slice)和切块(dice)：切片是在立方体的一个维上进行选择，如选择time="Q1"的数据；切块是在多个维上进行选择
- 转轴(pivot)：转动数据视角

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211208214251661.png" alt="image-20211208214251661" style="zoom:67%;" />

### 1.3.2 星形模式

&emsp;&emsp;包括一个大的中心表(事实表)和一组小的附属表(维表)，每维一个。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211208215333921.png" alt="image-20211208215333921" style="zoom: 67%;" />

### 1.3.3 雪花型模式

&emsp;&emsp;在星形模式的基础上，把数据进一步分解到附属表中。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211208215539851.png" alt="image-20211208215539851" style="zoom:67%;" />

# 2 聚类

&emsp;&emsp;聚类属于无监督学习的一种，是对没有类别(标签)的数据进行聚集，同一簇中的数据彼此相似，属于同一类别。聚类算法越好，簇内的相似度越高，簇间的相似度越低。

&emsp;&emsp;聚类的数据结构主要有两种，一是数据矩阵，其中每一行代表一个样本，每一列代表一种属性，

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206104552743.png" alt="image-20211206104552743" style="zoom:50%;" />

二是相异度矩阵，代表的是两个样本之间的相似性度量d(i,j)，

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206104836148.png" alt="image-20211206104836148" style="zoom:50%;" />

&emsp;&emsp;数据标准化，对于一个样本x<sub>f</sub>，计算其平均绝对偏差，

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206105300686.png" alt="image-20211206105300686" style="zoom: 67%;" />

其中，

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206105325962.png" alt="image-20211206105325962" style="zoom:67%;" />

也可以计算其标准偏差，

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206105433584.png" alt="image-20211206105433584" style="zoom:67%;" />

## 2.1 相似性度量

&emsp;&emsp;相似性度量包括样本间的相似性度量和簇间的相似性度量。

### 2.1.1 Minkowski(闵可夫斯基距离)

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211205001703203.png" alt="image-20211205001703203" style="zoom:67%;" />

&emsp;&emsp;x和y是两个p维的点，外面要开q次根。

### 2.1.2 Manhattan(曼哈顿距离)

&emsp;&emsp;闵可夫斯基距离中q=1，得到曼哈顿距离，

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211205001733590.png" alt="image-20211205001733590" style="zoom:67%;" />

### 2.1.3 Euclidean(欧几里得距离)

&emsp;&emsp;闵可夫斯基距离中q=2，得到欧几里得距离，又称欧式距离，

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211205001821133.png" alt="image-20211205001821133" style="zoom:67%;" />

### 2.1.4 簇间的相似性度量

- 最小距离

两个簇距离最近的两个点的距离。
$$
d_{min}(Ci,Cj)=min(|p−q|) {\quad} p∈Ci,q∈Cj
$$
<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211205002422476.png" alt="image-20211205002422476" style="zoom:50%;" />

- 最大距离

两个簇距离最远的两个点的距离。
$$
d_{max}(Ci,Cj)=max(|p−q|) {\quad} p∈Ci,q∈Cj
$$
<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211205002547030.png" alt="image-20211205002547030" style="zoom:50%;" />

- 均值距离

两个簇内先找平均节点，对平均节点求距离。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211205002801037.png" alt="image-20211205002801037" style="zoom:50%;" />

- 平均距离

两个簇所有节点间的距离的平均值。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211205003243033.png" alt="image-20211205003243033" style="zoom:50%;" />

## 2.2 基于划分的聚类

&emsp;&emsp;优点是算法简单，缺点是不能很好地处理噪音及孤立点，而且聚类效果对于初始值的选取有很大的依赖性。

### 2.2.1 K-Means

(1)对一组样本随机生成k个初始聚类中心

(2)每个样本归到距离最小的聚类中心对应的类别中

(3)随后每个类别重新计算聚类中心，为该类的质心(平均值)

(4)重复23，直到满足条件(迭代次数、最小误差变化等)

### 2.2.2 K-Medoids

&emsp;&emsp;K-Means算法中，新的中心可以是样本之外的点，一个具有很大极端值的样本会扭曲数据分布，造成算法对极端值敏感，而K-Medoids算法选择的样本必须是样本点，就相当于平均数和中位数的差别，能够降低噪声和孤立点的影响。

(1)在样本点中随机选取k个点作为初始聚类中心

(2)将剩余点归到距离最小的聚类中心对应的类别中

(3)在每一类中，计算各个成员点到其他成员点的距离之和，选最小的作为新的聚类中心

(4)重复23，直到聚类中心不再变化，或已达到设定的最大迭代次数

&emsp;&emsp;该算法的缺点是时间复杂度较高，对大数据集处理较慢。

## 2.3 基于层次的聚类

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211204235720905.png" alt="image-20211204235720905" style="zoom: 50%;" />

### 2.3.1 AGNES

&emsp;&emsp;属于凝聚的层次聚类，自底向上，最开始每个样本各属于一类，然后按照规则将相似的逐步合并。

(1)每个样本作为一个初始簇

(2)计算每两个簇间的距离，并找到最近的两个簇

(3)将这两个合并为新的簇

(4)重复23，直到满足终止条件(簇的个数达到设定；2中最相近的两个簇的距离超过阈值，不需要再合并)

### 2.3.2 DIANA

&emsp;&emsp;属于分裂的层次聚类，自顶向下，最开始各个样本都属于一类，然后按照规则逐步分裂。 簇的直径：在一个簇中的任意两个样本都有一个欧氏距离，这些距离中的最大值是簇的直径

(1)所有样本当作一个初始簇

(2)选出具有最大直径的簇

(3)找出这个簇中距离其他节点平均距离最大的一个点放入新簇c1，剩下的点放入新簇c2

(4)再c2中找出离c1距离更近的点，放入c1，直到没有可放的

(5)重复234，直到满足终止条件

### 2.3.3 BIRCH

https://www.cnblogs.com/pinard/p/6179132.html

## 2.4 基于密度的聚类

&emsp;&emsp;这类算法不是根据元素与类之间的距离进行相似性判定，而是根据元素分布的密度进行划分，因此不存在基于距离判定文本相似性所造成的过多依赖文本分布形状的不足。如下图，K-Means会造成右图这样的聚类。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206113452521.png" alt="image-20211206113452521" style="zoom:67%;" />

&emsp;&emsp;基于密度的聚类，其判定依据是如果某个区域中点的密度大于设定的阈值，则将该点归属到与之相邻的聚类中。缺点是对设定的扫描半径及最小包含点数极其敏感，这两个参数的细微变动都会对聚类效果造成很大的影响，而这两个参数的选择没有规律可循。

### 2.4.1 DBSCAN

&emsp;&emsp;设样本集D={x1,x2,...,xm}，

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206122223664.png" alt="image-20211206122223664" style="zoom:33%;" />

- Eps：邻域的最大半径，对于样本xi，只有d(xi,xj)≤Eps的样本xj才属于xi的邻域，图中圆圈代表邻域
- MinPts：邻域中样本个数的最小值，对于样本xi，当其邻域中样本的个数≥MinPts时，xi称为**核心对象**(红点)
- 密度直达：xi邻域中的点与xi是密度直达的
- 密度可达：通过密度直达的核心对象相连的样本是密度可达的，即图中绿色箭头
- 密度相连：密度可达的样本及其邻域内的样本是密度相连的

DBSCAN的思想就是将密度相连的样本聚为一类。算法步骤为：选择一个没有类别的核心对象，找到与其密度相连的样本聚为一簇，继续选没有类别的核心对象寻找其密度相连的样本，直到所有核心对象都有类别为止。一些异常样本点或者说少量游离于簇外的样本点，不在任何一个核心对象的周围，一般将这些样本点标记为噪声点。

# 3 关联规则挖掘

&emsp;&emsp;找出数据集中频繁出现的数据组合，找出这些组合有助于我们做一些决策。例如，什么商品组合顾客会在同一次购物中购买，这就是购物篮分析，可以帮助门店的销售过程中找到具有关联关系的商品，并以此获得销售收益的增长。

- 支持度(Support)：事件同时发生的概率P(AB)
- 置信度(Confidence)：在事件A发生的基础上，发生事件B的概率P(B|A)=P(BA)/P(A)
- 频繁k项集：频繁项集指的是在数据集中频繁出现的项集，若项集中有k个元素，则称k项集，若k项集出现的次数≥支持度阈值，则称频繁k项集

## 3.1 寻找最大频繁k项集

&emsp;&emsp;找到超过设定支持度的最大的频繁k项集，最大指的是k最大。

### 3.1.1 Apriori

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206192906600.png" alt="image-20211206192906600" style="zoom:50%;" />

&emsp;&emsp;**任何非频繁项集的超集也一定是非频繁的**，可以利用这一点进行剪枝，所有非频繁项集的超集都不用进行测试。如上图所示，设支持度阈值为50%，共4组数据，即至少出现2次。首先搜索出1项集及对应的支持度C1，剪枝去掉低于支持度阙值的1项集，得到频繁1项集L1；然后用L1进行连接得到2项集C2，并进行剪枝，得到频繁2项集L2；以此类推，迭代下去，直到无法找到频繁k+1项集为止；最终得到L3{2 3 5}。

参考：[Apriori算法是什么？适用于什么情境？](https://www.zhihu.com/question/19912364/answer/963934469)

### 3.1.2 FP-Tree

&emsp;&emsp;Apriori算法简单，易于实现，但是当数据集很大的时会出现下面两个问题： 需要多次扫描数据集；可能会产生庞大的候选集，速度会很慢。FP-Tree算法对数据集仅需扫描两次，性能得到了提升。

&emsp;&emsp;首先要建立项头表，其中记录了频繁1项集出现的次数，按照次数降序排列。第一次扫描数据集就是建立项头表，第二次扫描数据集，是将读到的原始数据剔除非频繁1项集，并按照支持度降序排列。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206210124725.png" alt="image-20211206210124725" style="zoom: 33%;" />



上图中，ABCEFO剔除了非频繁1项集{O}，得到ABCEF，然后按支持度排列，得到ACEBF，其他数据以此类推，排序是为了FP树的建立时，可以尽可能的共用祖先节点。

&emsp;&emsp;随后就要建立FP-Tree，一条条读入排序后的数据集，插入FP树，插入时按照排序后的顺序，插入FP树中，排序靠前的节点是祖先节点，而靠后的是子孙节点。如果有共用的祖先，则对应的公用祖先节点计数加1。插入后，如果有新节点出现，则项头表对应的节点会通过**节点链表**链接上新节点。直到所有的数据都插入到FP树后，FP树的建立完成。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206210502857.png" alt="image-20211206210502857" style="zoom: 25%;" />

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206210539704.png" alt="image-20211206210539704" style="zoom:25%;" />



<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206210605873.png" alt="image-20211206210605873" style="zoom:25%;" />



最终得到，

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206210642897.png" alt="image-20211206210642897" style="zoom:25%;" />

&emsp;&emsp;最后就是挖掘最大频繁k项集，要从项头表的底部向上逐个进行，即先F然后D，最后A。对每一项，要找其条件模式基，所谓条件模式基是以该项作为叶子节点所对应的FP子树，得到这个FP子树，我们将子树中每个节点的的计数设置为叶子节点的计数(计数主要是为了删除)之和，叶子节点的初始值是原始FP-Tree中的值而不是1，并删除计数低于支持度阈值的节点。从这个条件模式基，我们就可以递归挖掘得到频繁项集了。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206211131853.png" alt="image-20211206211131853" style="zoom:25%;" />

&emsp;&emsp;对F来说，其FP子树的叶子节点就是F，各项都设计数为2，均不低于阈值，则F对应的最大频繁集为5项集{A C E B F}。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206211458909.png" alt="image-20211206211458909" style="zoom:25%;" />

&emsp;&emsp;对D，得到如上子树，E和G的叶子节点为均为1个D:1，计数设为1，A和C的叶子节点均为2个D:1，计数设为2，则删掉计数低于阈值的E和G，得到{A C D}，当前节点D要保留。**找叶子节点设计数的时候要注意图中的虚线和实线，虚线是节点链表，实线才连到叶子节点。**还要注意两个分支可以合并的情况。

&emsp;&emsp;对其他节点也是一样，最终，最大的频繁项集为5项集{A C E B F}。

参考：[FP Tree算法原理总结](https://www.cnblogs.com/pinard/p/6307064.html)

## 3.2 生成关联规则

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211206193624056.png" alt="image-20211206193624056" style="zoom:50%;" />

&emsp;&emsp;对找到的每个频繁项集，生成其所有的非空子集，计算置信度，如上图所示，若置信度阈值为70%，则只有第2、3、6个规则可以作为最终的输出。

# 4 链接挖掘

## 4.1 PageRank

&ensp;&ensp;  PageRank是由Google发明的用于对网页重要性进行排序的算法。该算法基于两个假设，一是一个网页接收到的其他网页指向的入链(in)越多，说明该网页越重要；二是当一个质量高的网页指向(out)一个网页，说明这个被指向的网页质量也高。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211128103556556.png" alt="image-20211128103556556" style="zoom:67%;" />

最原始的计算公式为，
$$
PR(A)=∑PR(Ti)/Out(Ti)
$$
PR(A)网页A的PageRank值，Ti代表指向A的页面，Out(Ti)代表Ti的出度，各节点的PR值都初始化为1，然后迭代，直到迭代变化的值很小。对于上图，第一次迭代时，PR(A)=PR(C)/Out(C)+PR(D)/Out(D)=1/2+1/1=1.5，以此类推(至于是先从A还是先从B、C、D开始算，都可以，结果不是唯一的，但对于多次迭代来说，结果都可以落在可接受的范围内)。该公式还可以使用矩阵化表达，快速计算，
$$
PR(A)=M*V
$$
M是马尔科夫矩阵，是根据边的连接情况构成的，V是上一次的PageRank的向量。

<img src="https://raw.githubusercontent.com/Forest216/cloud-image/main/image-20211128105326979.png" alt="image-20211128105326979" style="zoom: 50%;" />

然而，这会出现Spider Traps问题，当某个页面含有闭环，即自己指向自己时，经过多次循环，其PR值会归为1，而其他网页归为0，因此对公式进行修正，
$$
PR(A)=(1-d)+d*(∑PR(Ti)/Out(Ti))
$$
其中，d代表阻尼系数，d代表继续浏览其他页面的概率，一般设为0.85，(1-d)代表停留在当前页面的概率。

&ensp;&ensp;&ensp;  PageRank的缺点是可以通过"僵尸网站"或链接，人为刷PageRank值。

&ensp;&ensp;&ensp;  参考：[浅谈PageRank算法](https://zhuanlan.zhihu.com/p/197877312)

## 4.2 HITS算法

https://www.lovelucy.info/pagerank-sns-model-1.html

