# Visualizing a Decision Tree 
> Google Machine Learning Recipes 2

## Why decision Tree
### Many types of classifiers

* Artificial neural network - 神经网络
* Support Vector Machine - 支持向量机(支持向量网络)
* Lions
* Tigers
* Bears

### 决策树好处
- Easy to read and understand
- 仅有的可解释的几种模型之一（能理解分类器做决策的过程）

> 决策树就是一系列关于feature的判断作为结点，以label为叶子的一棵树。因此feature越好，结果也越好。

## Iris

### 经典机器学习问题：[识别三种Iris](https://en.wikipedia.org/wiki/Iris_flower_data_set)

可以在维基看到这个数据集的详细信息，共 50 * 3 = 150 条记录

### 四个feature：

* Sepal length
* Sepal width
* Petal length
* Petal width

### 三个label：

* setosa
* versicolor
* virginica

可以从[sklearn](http://scikit-learn.org/stable/datasets/)中直接导入。

### **组成**

* metadata: feature_names, target_names(这个其实就是label names)，描述数据用
* data: 具体feature数据，是一个数组，数组中的每个元素是dataset中的一条数据
* target: 具体label数据，是一个数组

## 目标
1. 导入数据
2. 训练分类器
3. 预测新的花的label
4. 查看决策树

## 测试数据

- 非训练数据的真实数据，测试分类器的准确度，
- 这里从dataset中抽出第0，第50，第100条作为测试数据
- numpy是一个Python的数据处理库，查看官方[Tutorial](https://docs.scipy.org/doc/numpy-dev/user/quickstart.html)学习更多
- 测试有很多内容，后面还会有。

## 环境
### Linux 下可以参考这个：
可视化使用了 pydot，但 Pycharm 会升级 anaconda 中的包，导致找不到，我执行了
```
sudo /home/cwh/anaconda2/bin/conda install -p /home/cwh/anaconda2 pydot -y
```
重新安装 pydot 修复 pydot 找不到的问题；

另外 pydot 会找不到 Graphviz ，需要再安装
```
sudo /home/cwh/anaconda2/bin/conda install -p /home/cwh/anaconda2 Graphviz -y
```
然后将 Graphviz 添加到环境变量中，修改 /etc/environment 为以下内容，重启系统（我的系统是 Ubuntu14.04LTS ）：
```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/home/cwh/android-sdk-linux/ndk-bundle:/home/cwh/android-sdk-linux/platform-tools:/home/cwh/anaconda2/pkgs/graphviz-2.38.0-1/bin"
```

然后又会有 Graphviz 中找不到 libgvplugin_pango.so.6 的问题，根据[官网 Issue 的解答](http://www.graphviz.org/content/issue-warning-could-not-load-usrlibgraphvizlibgvpluginrsvgso6)，应该是少了依赖库
```
ldd /home/cwh/anaconda2/pkgs/graphviz-2.38.0-1/lib/graphviz/libgvplugin_pango.so.6
```

发现 libpng16 not found ，于是安装 libpng16，在[这里](https://sourceforge.net/projects/libpng/?source=directory)下载，然后安装，

```
./configure
make
sudo make install
sudo ldconfig
```
再运行代码即可。

### Windows 下可以参考这个:

教程中的代码采用的是：

    graph.write_pdf("iris.pdf")
    
会报 `AttributeError: 'list' object has no attribute 'write_pdf'` 错误

显然`pydot.graph_from_dot_data`返回的是 list (至于为什么教程可以通过我暂时也不知道，如果你知道请一定告诉我)，所以应该用：

    graph[0].write_pdf("iris.pdf")

如果你在用一个 Python 的新版本，可以尝试用 pydotplus .

    import pydotplus
    ...
    graph = pydotplus.graph_from_dot_data(dot_data.getvalue())
    graph.write_pdf("iris.pdf")
    

如果报了这个错：

    Error “GraphViz's executables not found” when calling GraphViz layout from NetworkX in iPython notebook

请先安装 GraphViz.msi ，再将/bin/目录放进环境变量，再运行代码

如果还报这个错误，请添加以下代码，设置PATH：

    import os     
    os.environ["PATH"] += os.pathsep + 'C:/Program Files (x86)/Graphviz2.38/bin/'

## Code (以Iris为例，导入数据，训练分类器，预测，查看决策树)
    import numpy as np
    import pydot
    import pydotplus
    import os
    os.environ["PATH"] += os.pathsep + 'C:/Graphviz2.38/bin/'
    
    from sklearn.datasets import load_iris
    from sklearn import tree
    from sklearn.externals.six import StringIO
    
    iris = load_iris()
    print iris.feature_names
    print iris.target_names
    # print iris.data[0]
    # print iris.target[0]
    # for i in range(len(iris.target)):
    #     print("Example %d : label %s, features %s" %
    #           (i, iris.target[i], iris.data[i]))
    
    test_idx = [0, 50, 100]
    
    # training data
    train_target = np.delete(iris.target, test_idx)
    train_data = np.delete(iris.data, test_idx, axis=0)
    
    # testing data
    test_target = iris.target[test_idx]
    test_data = iris.data[test_idx]
    
    # train
    clf = tree.DecisionTreeClassifier()
    clf.fit(train_data, train_target)
    
    # test
    print test_target
    print clf.predict(test_data)
    
    # visual code
    
    dot_data = StringIO()
    tree.export_graphviz(clf,
                         out_file=dot_data,
                         feature_names=iris.feature_names,
                         class_names=iris.target_names,
                         filled=True, rounded=True,
                         impurity=False)
    
    graph = pydot.graph_from_dot_data(dot_data.getvalue())
    # graph.write_pdf("iris_decision_tree.pdf") # return a list
    graph[0].write_pdf("iris2.pdf")
    # graph = pydotplus.graph_from_dot_data(dot_data.getvalue())
    # graph.write_pdf("iris.pdf")
    
    print test_target
    print test_data
