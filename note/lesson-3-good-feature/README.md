# What Makes a Good Feature

> Google Machine Learning Recipes 3


> 分类器的优秀之处只在于你所提供的各样不同特性，这意味着具备好的特性(Feature)是你在机器学习里其中最重要的工作。

## 什么造就好的 Feature

* 在二分类中，一个好的 Feature 使它可以很容易在两个不同的事物之间做决定

### 假设我们要撰写一个分类器用来分辨两种类型的狗，两个的 Feature ：
* 身高(英寸)
* 眼睛的颜色

### 如何判断是否为好的 Feature 呢？
* 如果说一个品种的狗通常比另一品种的狗高，那么说明身高这个 Feature 是一个好的 Feature 。
* 如果说眼睛的颜色不是取决于品种，换句话说，我们不能通过这个 Feature 去很好的区别品种，那么这个 Feature 不是一个好的 Feature，假设训练数据内包含一个像这样无用的  Feature，可能会破坏分类器的准确度，特别是在训练数据不多的情况下。

> 但是事情总有特例，我们不能不认为第一个品种的狗总是比第二个品种的狗高，所以当我们想到一个 Feature 的时候，**必须考虑它在一个种群中的不同情况**

* 以上两点证明了**好的feature能有力地说明两个类别的不同**


* 单个 Feature 往往不完美，所以需要多个 Feature 
* 假如由人来做分类器，会需要什么信息？(找好的 Feature )
* 对于一个 Feature ，如果不同的 label 中，这个 Feature 的值分布越均匀，则这个 Feature 的分类作用越弱

> 在同一种眼睛颜色中，不同狗的数量差不多，说明眼的颜色的分类作用弱，这样的 Feature 会降低分类器的准确性

* 好的 Feature 应该是相互独立的，能够提供更多有效信息，
* 每个 Feature 在分类器中都占一定的重要性，而如果  Feature 间不独立，重要性的比重也会与原本的计划有偏差
*  Feature 应当预处理地尽可能与结果直接相关
* 有好的 Feature 还不够，还要有好的 Feature 之间的好的组合

## **总结**
好的 Feature 应该是这样的：

* Informative (资料丰富)
* Independent (独立的，英寸和厘米都表示身高，所以只能代表一个 Feature )
* Simple 

## Code(构造数据集与绘制柱状图)

    import numpy as np
    # to change the matplotlib backend from agg to tkagg : start
    import matplotlib
    matplotlib.use('TkAgg')
    # to change the matplotlib backend from agg to tkagg : end
    import matplotlib.pyplot as plt
    
    greyhounds = 500
    labs = 500
    
    grey_height = 28 + 4 * np.random.randn(greyhounds)
    lab_height = 24 + 4 * np.random.randn(labs)
    
    
    plt.hist([grey_height, lab_height], stacked=True, color=['r', 'b'])
    plt.show()

> matplotlib 默认的 backend 是 agg ,无法渲染图，改为  TKAgg 即可，参考[来源](http://www.jianshu.com/p/3f4b89aaf057)。

> 如果觉得我的文章对您有帮助，请随意打赏～

<img src="https://github.com/ahangchen/GoogleML/raw/master/res/wxmoney.jpg" width = "400" height = "400" alt="图片名称" align=center />
