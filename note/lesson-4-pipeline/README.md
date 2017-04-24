# Let’s Write a Pipeline
> 转载请注明作者：[梦里风林](https://github.com/ahangchen)

> Google Machine Learning Recipes 4

## 回顾并强化概念

### 编写一个基础 Pipeline 进行监督学习

- 监督学习基础套路
    - 例子： 一个垃圾邮件分类器
    > 关键在于标记刚收到的邮件是否为垃圾邮件

    - Train vs Test：在实验中，将数据分成训练集和测试集，训练集负责训练模型，而测试集负责验证训练的准确度
    - 特征 X 与标签 Y： 我们可以把分类器看成是一种函数f(x) = y
    > feature: x,label:y
    classifier 其实就是一个feature到label的函数

    - 可以从sklearn中import各种分类器( tree, KNeighborsClassifier )进行训练，各种分类器有类似的接口( fit, predict )
    > 这些不同分类器都可以解决类似的问题

### Code(a Pipeline)
    # import a dataset
    from sklearn import datasets
    iris = datasets.load_iris()

    X = iris.data
    y = iris.target

    from sklearn.model_selection import train_test_split

    # DeprecationWarning: This module was deprecated in version 0.18 in favor of the model_selection module into which all the refactored classes and functions are moved. Also note that the interface of the new CV iterators are different from that of this module. This module will be removed in 0.20.

    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=.5)

    # compare the predicted labels to the true labels

    # from sklearn import tree
    # my_classifier = tree.DecisionTreeClassifier()

    # use another classifier
    from sklearn.neighbors import KNeighborsClassifier
    my_classifier = KNeighborsClassifier()

    my_classifier.fit(X_train, y_train)

    predictions = my_classifier.predict(X_test)
    # print predictions

    # compare the predicted labels to the true labels
    from sklearn.metrics import accuracy_score
    print accuracy_score(y_test, predictions)

> 在0.20或以上的版本，用 model_selection 代替 cross_validation

### 关于一个算法从数据中学习的真正含义

 - 拒绝手工写分类规则代码
  - 本质上，是学习feature到label，从输入到输出的函数
  - 从一个模型开始，用规则来定义函数
  - 根据训练数据调整函数参数
  - 从我们发现规律的方法中，找到model
  - 比如一条划分两类点的线就是一个分类器的model，调整参数就能得到我们想要的分类器：
![](leanote://file/getImage?fileId=58fda16f14e0c23c48000000)
  - [TensorFlow PlayGround](http://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=4,2&seed=0.61429&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification)

  > Example of Neural Network

- [sklearn 笔记](https://github.com/ahangchen/GDLnotes/tree/master/note/sklearn)

> 觉得原作者(ahangchen)的文章对您有帮助的话，就给个[star](https://github.com/ahangchen/GDLnotes)吧～
