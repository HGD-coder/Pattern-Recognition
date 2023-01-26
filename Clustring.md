---
title: 机器学习西瓜书学习笔记【第九章】
date: 2021-2-11 12:00:03
tags: [理论学习,机器学习,西瓜书,聚类,K-means,DBSCAN,高斯混合聚类]
toc: True
---

# 第9章  聚类

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/image-20210210014655191.png)

<!--more-->

## 9.1 聚类任务

> **什么是聚类任务？**

- **类别：**无监督学习
- **目的：**通过对无标记训练样本的学习来揭示数据的内在性质及规律，为进一步的数据分析提供基础。

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210151558.png)

## 9.2 性能度量

> **什么是好的聚类？**

- **目的：**① 评估聚类结果的好坏 ② 确立优化的目标
- **结论：**簇内的样本尺度尽可能彼此相似，簇间的样本尽可能不同。

### 9.2.1 外部指标

- **外部指标：**将聚类结果与某个 “参考模型” 进行比较，称为 “ 外部指标 ”。

  ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210209195423.png)

  ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210209194620.png)

  ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210209194628.png)

  ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210209194608.png)

  -  <img src="https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210209194658.png"  />

    > ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/0C250F758C147E79F8349A7C2B61D1B5.jpg)

### 9.2.2 内部指标

- **内部指标：**直接考察聚类结果而不利用任何参考模型，称为 “ 内部指标 ”。

  ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210209195511.png)

  ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210209194806.png)

  ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210209194829.png)

  - ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210209195003.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/9019575AF193CD34EACE30F9281FD792.jpg)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/6CB6BA508A1120B90236536102DFEDB2.jpg)

​	![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/FC43D917BDC83C8C49338D5FDCF4F3CC.jpg)

### 小结

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210011144.png)

## 9.3 距离计算

> **样本间距离怎么确定？**

### 9.3.1 距离度量 / 非距离度量

- 若它是一个 “ 距离度量 ”，则应该满足以下性质：

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210004316.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210004325.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210015553.png)

### 9.3.2 有序属性 / 无序属性

#### **有序属性**

- ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210004639.png)
- **欧氏距离：**
  - <img src="https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210004755.png" style="zoom:50%;" /><img src="https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210004814.png" style="zoom: 67%;" />
- **曼哈顿距离：**
  - <img src="https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210004921.png" style="zoom: 80%;" /><img src="https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210004931.png" style="zoom: 67%;" />
-  **切比雪夫距离：**
  - ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210005157.png)

#### 无序属性

- ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210011512.png)

  

#### 混合距离

- ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210011545.png)

#### 加权距离

- ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210011625.png)

### 小结

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210010706.png)

## 9.4 原型聚类

> ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210015648.png)

### 9.4.1 k 均值算法

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/1234333422.gif)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20201018202041.png)

- **步骤：**
  - 随机选取样本作为初始均值向量（初始值：k 的值【即几个簇】）
  - 分别计算每个样本点到初始均值向量的距离，距离哪个点最近就属于哪个簇
  - 每个簇重新计算中心点，重复第二步直到收敛

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210021340.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210021518.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210021531.png)

### 9.4.2 学习向量量化

> 和 K-means 的不同：
>
> - 每个样例有类别标签，即 LVQ 是一种监督式学习；
> - 输出不是每个簇的划分，而是每个类别的原型向量；
> - 每个类别的原型向量不是简单的均值向量，考虑了附近非 / 同样例的影响。

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210040052.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210034610.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210034804.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210035001.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210035012.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210035139.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210035151.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210035424.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210035433.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210035539.png)

**例题：**

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210041038.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210041102.png)



### 9.4.3 高斯混合聚类

原先数据集是这个样子的：

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210161020.png)

某天，被黑客入侵，把两个数据集混合起来了，要怎么分开呢？

<img src="https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210161036.png" style="zoom:80%;" />

首先，我们确定了要分成两个高斯模型，我们随机选取两个 **均值** 和 **方差** 作为初始值

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210161327.png)

之后，我们分别分析每个点对两个高斯模型的隶属度

<img src="https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210161404.png"  />

做完以后，我们得到越红的点对红色高斯模型的隶属度越高，越绿对绿模型隶属度越高

<img src="https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210161455.png" style="zoom:80%;" />



隶属度又对模型本身的 均值 和 方差 造成影响，于是我们得到了 一次迭代后的 两个高斯模型，可以发现红圈基本没动，绿圈向右上方移动了一点

<img src="https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210161648.png" style="zoom:125%;" />

多次迭代的动画是这样的。

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/1234.gif)

但是通过最开始的数据，我们知道我们的目的是找到下面的两个数据集【黄圈】

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210162734.png)![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/image-20210210162747880.png)

显然我们这次高斯聚类并不成功，这是由于我们给了它不好的初始值【随机值】，所以我们重新做一次，打算来手动输入初始值，那初始值怎么设定呢？我们选择，先用 K 均值的方法，来选定两个中心值，把这两个中心值作为我们的手动输入值，结果变成了这样。

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/1234.gif)

我们发现还是没达到我们想要的效果，因此我们下一步不再使用简单的圆高斯模型，使用协方差矩阵，而不是每个高斯的方差，这样可以使圆圈变成椭圆形

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/12343334.gif)

到这里我们只是直观上对高斯模型有个了解，还有一些疑问，比如：图中的圈都带表什么呢？

这是一次期中考试的学生成绩分布，很明显他是属于高斯分布（正态分布）的

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210164044.png)

画成柱状图是这样的

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210164149.png)

经过简单的计算 **均值** 和 **方差** 我们能够描绘出他的高斯曲线

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210164240.png)

μ 代表平均数，也就是平均成绩

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210164334.png)

其次是标准差，这个例子中，标准差是15，这很容易计算	

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210164354.png)

我们发现 【均值 - 1个标准差】 和 【均值 + 1个标准差】，这段区域占总数的 68％，这是高斯分布的属性

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210164532.png)

而 【均值 - 2个标准差】 和【 均值 + 2个标准差】，这段区域占总数的 95％

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210164637.png)

【均值 - 3个标准差】 和【 均值 + 3个标准差】，这段区域占总数的 99％

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210164715.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210165006.png)

知道了圈代表什么，还有一个问题，高斯模型我们知道，那高斯混合模型是什么意思呢？

我们看，这里有一个班级的两门课成绩，分别是物理和生物，数轴是以 20 为单位的，我们发现这次生物题比较简单，全班分数都挺高，而物理题比较难，全班成绩都低

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210165423.png)

我们把数据绘制成柱状图，通过柱状图我们发现他们都遵循高斯分布，尽管 均值 和 方差 不同，但都是高斯分布

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210165703.png)

假如就是这个数据集，我们想对它做高斯混合聚类处理，数据叠加到一起是这样的，它是一个模型，但并不是一个高斯分布，它是两个子集和合并，但合并之后并不是高斯分布

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210165821.png)

它是两个没有标签的高斯分布

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210170041.png)

经过计算机的高斯混合聚类，我们得到了这样的结果

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210170135.png)

到这里我们知道了，高斯混合分布本身并不是高斯模型，而是两个高斯模型的混合物，哪个点更可能属于哪一个高斯模型，它就被分到哪一个类中，这就是高斯混合模型的最简单的例子。

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210165915.png)

#### 步骤

1. 初始化 高斯混合成分的个数 k ，假设高斯混合分布模型参数 **α(高斯混合系数)**  **μ (均值) ,  Σ(协方差矩阵)**；
2. 分别计算每个样本点的 后验概率 (该样本点属于每一个高斯模型的概率)；
3. 迭代 **α**    **μ ,  Σ；**
4. 重复第二步直到收敛。

#### 难点

- 后验概率 (该样本点属于每一个高斯模型的概率)的计算：
  - ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210173640.png)
    - 上述公式由 7.18 相减化简而来![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210173904.png)
  - ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210173654.png)
  - ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210173815.png)
  - ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210173846.png)
- 怎样迭代 **α**    **μ ,  Σ；**
  - **α**  ——通过样本加权平均值来估计
    - ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210174242.png)
  - **Σ** ——通过样本加权平均值来估计
    - ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210174336.png)
  - **μ** ——由样本属于该成分的平均后验概率确定
    - ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210174515.png)

#### 例子

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210175003.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210175018.png)

#### EM思想的体现

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210175114.png)

### 小结

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210175755.png)

## 9.5 密度聚类

![](https://miro.medium.com/max/675/1*tc8UF-h0nQqUfLC8-0uInQ.gif)

> ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/image-20210210014816353.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20201018201435.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210022341.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210022631.png)

**例题：**初始值：①邻域参数 ε      ② 最少点个数 MinPts 

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210023731.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210024227.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210024246.png)



## 9.6 层次聚类

![](https://miro.medium.com/max/700/1*ET8kCcPpr893vNZFs8j4xg.gif)

> ![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/image-20210210014916753.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210024814.png)![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210024822.png)



![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210024731.png)

<img src="https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20201103192551.png" style="zoom:67%;" />



**例题：**

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210025032.png)

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210025043.png)

## 总结

![](https://gavin-pic-1302578220.cos.ap-beijing.myqcloud.com/img/20210210180215.png)