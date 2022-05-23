---
title: DeepLearning
description: 李宏毅DeepLearning Loss Function比较
categories: DeepLearning
tags:
- DeepLearning

---

## 各种Loss function比较

### SDG

最初的梯度下降法

### SDGM:Optimize

momentum:考虑上一次的移动方向，此次移动方向为梯度与上次移动方向的加权和（即考虑了历史梯度）。

Learning rate:随时间变化

### Adagrad

Learning rate 的分母：之前梯度平方的和开根号 ，想象一下比较陡（grad较大）的曲线一下子走太大的步子是不是不太好，所以通过控制learning rate的大小 控制步伐的大小。若之前的grad较小，则可以把步子放大点（分母值变小了）。 

### RMSProp：

与Adagrad类似，只是分母改成了梯度的加权平方和，参考momentum思想。多了一个hyperparamter:a,可以调a来控制。（a=0.1)

### Adam

SGDM+RMSProp,即将RMSProp的grad改成SGDM的grad项。

**结论：adam训练比较快，但是泛化能力不一定如sdgm。**



### Batch normalization

error surface 为椭圆形 --->因为不同参数对应的feature的范围不一样，所以将feature normaliztion，而feature normalization需要多个example（算均值、方差），若example总量为几万个，那么无法一次性读取，所以选择batch，batch_size = 64。这样相当于有64个网络分别训练64个examples,之后对每个feature算均值（求和/64）

### Softmax

神经网络的最后一层，对每个输出值取e,之后/e总和