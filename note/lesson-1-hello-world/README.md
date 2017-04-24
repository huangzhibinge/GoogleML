# Hello world
> Google Machine Learning Recipes 1
### 需要用到的库
* scikit-learn
* TensorFlow

### 机器学习是什么
> 我们可以把机器学习看做是人工智能的一个子领域

> 相对于初期的人工智能程序只能做好一件事，机器学习可以同时做好多件事情，比如阿尔法狗擅长围棋，同时也可以玩其他游戏。

> 那么机器学习是怎么做到的呢？
> 它的算法可以从样本和经验中学习，而不是依靠硬编码的规则。

## Supervised learning
> 用来实现自动分类器的技术即监督学习

原本我们是教会机器我们的规则，由机器执行规则进行分类，识别。

但规则总有漏洞，我们总能举出规则的反例。

我们不能为每种反例都对规则做修正，那是个无底洞。

所以我们让**机器自己学习规则**。

## Classifier(分类器)
> 接受一些数据作为输入，然后给它们分配标签作为输出

* Input: Data (features)
* Output: class (label)

## 监督学习的过程(区分苹果和橘子)

> 我们将描述的水果属性作为输入数据，然后根据像重量，质感等特性，对收集到数据进行预测

* 收集训练数据： examples

> 我们需要从data中，提取出可以作为分类依据的特征作为feature

* 训练分类器： 分类器有很多种，我们这个部分使用了决策树
* 进行预测

## 环境搭建


使用[scikit-learn](http://scikit-learn.org/stable/index.html)做Python上的机器学习；

官网推荐使用[Anaconda](https://www.continuum.io/downloads)进行安装，轻松解决依赖，有两个版本可以用，我使用[Python2版本](http://repo.continuum.io/archive/Anaconda2-4.0.0-Linux-x86_64.sh), 因为许多库只支持python2, 而且教程使用的也是python2

安装后，关联Pycharm，新建一个工程，选择interpreter为anaconda里的python，这样才能顺利引用机器学习的库；

> 如果已经选了其他编译器，需要在File - Settings - 搜索interpreter，修改。

笔者的环境是Sublime text 3,偷个懒，扔几篇网上的教程:

* [Sublime Text 3 下搭建python IDE环境 --Anaconda插件篇](http://www.cnblogs.com/nx520zj/p/5787393.html)
* [Sublime Text 3 装了Anaconda 写Python代码出现框框的解决办法](http://blog.csdn.net/kinglearnjava/article/details/49307463)
* 安装完Anaconda，还要将默认编译系统的地址改为Anaconda，它自己会去找到第一个教程配置的 `python.exe` :
  [配置Sublime Text 3 的Anaconda编译环境](http://blog.csdn.net/zhihaoma/article/details/50917915)


## Code(一个简单的分类器训练与预测)
    from sklearn import tree
    features = [[140, 1], [130, 1], [150, 0], [170, 0]]
    labels = [0, 0, 1, 1]
    clf = tree.DecisionTreeClassifier()
    clf = clf.fit(features, labels)
    print clf.predict([[150, 0]])


> 如果觉得原作者(ahangchen)的文章对您有帮助，请随意打赏～

<img src="https://github.com/ahangchen/GoogleML/raw/master/res/wxmoney.jpg" width = "400" height = "400" alt="图片名称" align=center />