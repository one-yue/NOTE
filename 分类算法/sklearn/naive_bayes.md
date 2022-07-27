# naive_bayes

## 1. BernoulliNB 伯努利贝叶斯

适用于离散数据，针对二分类设计的分类方法

## 2. MultinomialNB 多项式朴素贝叶斯

适用于具有离散特征的分类。BernoulliNB和MultinomialNB方法类似，B是二分类，M是多分类或者二分类

## 3. ComplementNB 补码朴素贝叶斯

适用于不平整数据集，旨在纠正多项式贝叶斯分类器所做的“严重假设（seevere assumptions）”

## 4. CategoricalNB 分类朴素贝叶斯

适用于具有分类分布的离散特征的分类

## 5. GaussianNB 高斯朴素贝叶斯

适用于特征是连续数据，符合高斯分布

参数：

1. priors：先验概率，如果指定，则不会根据数据调整先验值
2. var_smoothing: float, default=1e-9
    
    所有特征中最大方差的一部分，为计算稳定性而增加到方差中。 