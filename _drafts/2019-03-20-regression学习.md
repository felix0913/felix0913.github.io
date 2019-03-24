---
layout: post
title:  "regression学习"
date:   2019-3-20 15:55
categories: MachineLearning
tags: ml regression 回归
---

* content
{:toc}


continuous Supervised Learning： 
- continuous指的是output




# 公式来源
X和Y可以使用如下方程式表示：
![](https://github.com/felix0913/felix0913.github.io/blob/master/_pic/regression-1.jpg?raw=true)

用向量表示，即为： X * w = Y

通过变换，
![](https://github.com/felix0913/felix0913.github.io/blob/master/_pic/regression-2.jpg?raw=true)

得到w的公式
![](https://github.com/felix0913/felix0913.github.io/blob/master/_pic/regression-3.jpg?raw=true)


# 误差来源：
- sensor error
- being given bad data
- transcription error 抄录时产生的错误
- unmodeled influences

# cross validation 交叉验证
- S折交叉验证会把样本数据随机的分成S份，每次随机的选择S-1份作为训练集，剩下的1份做测试集。
- 当这一轮完成后，重新随机选择S-1份来训练数据。
- 若干轮（小于S）之后，选择损失函数评估最优的模型和参数。