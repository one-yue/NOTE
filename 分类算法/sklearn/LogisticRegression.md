# LogisticRegression

## 1. 参数

### 1. penalty：正则化参数

取值(default:l2)：
```python
{'l1','l2','elasticnet','none'}
```
1. newton-cg、sag 和 lbfgs 算法只能使用 l2 正则化，因为L1正则化的损失函数不是连续可导的。
2. elasticnet是弹性网络正则化，是L1正则化和L2正则化的混合项，仅支持saga损失函数优化器。
3. 在调参时一般选择L2正则化就够了，但是如果选择L2正则化发现还是过拟合，即预测效果差的时候，就可以考虑L1正则化。另外，如果模型的特征非常多，我们希望一些不重要的特征系数归零，从而让模型系数稀疏化的话，也可以使用L1正则化。

### 2. solver 损失函数优化器

取值(default:lbfgs)：
```python
{'liblinear','lbfgs', 'sag','newton-cg', 'saga'}
```

solver参数决定了我们对逻辑规格损失函数的优化方式，有五种算法可以选择，分别是：
1. liblinear：使用了开源的liblinear库实现，内部使用了坐标轴下降法来迭代优化损失函数，适用于小数据集。
2. lbfgs：拟牛顿法的一种，利用损失函数二阶导数矩阵即海森矩阵来迭代优化损失函数。
3. newton-cg：也是牛顿法家族的一种，利用损失函数二阶导数矩阵即海森矩阵来迭代优化损失函数。
4. sag：即随机平均梯度下降，是梯度下降法的变种，和普通梯度下降法的区别是每次迭代仅仅用一部分的样本来计算梯度，适合于样本数据多的时候，sag是一种线性收敛算法，这个速度远比梯度下降法快。
5. saga：快速梯度下降法，线性收敛的随机优化算法的的变种，适用于样本量非常大的数据集。

总结：
```
1、liblinear支持L1和L2，只支持OvR做多分类。
2、lbfgs， sag，newton-cg只支持L2，支持OvR和MvM做多分类。
3、saga支持L1、L2、Elastic-Net，支持OvR和MvM做多分类。
```

### 3. multi_class 分类方式选择参数

取值(default:auto)：
```python
{'auto','ovr','multinomial'}
```

1. ‘ovr’ – ‘OvR’, 将多分类问题看成是二分类问题，每次只将一类样本与其他类样本组成的集合进行训练，进行 nc 次训练以后就可以完成多分类问题的处理了。
2. ‘multinomial’ – ‘MvM’，liblinear 不能选择该项，以单循环的方式进行分类，每次处理两个分类，保证样本中所有分类两两组合进行过一次训练，共需 nc*(nc-1)/2 次训练，分类速度慢，但分类结果更准确。
3. ‘auto’ – 如果 resolver 是 liblinear 则选择 OvR，否则选择 MvM。

### 4. class_weight 类型权重参数
 
取值(default:None)：
```python
{'dict','balanced'}
```

1. dict – 通过 dict 定义分类权重：{class_label: weight}。
2. balanced – 类库会根据训练样本量来计算权重。某种类型样本量越多，则权重越低，样本量越少，则权重越高。
3. None – 默认值，不指定权重。

### 5. dual 对偶或原始方法

bool类型，默认为False。对偶方法只用在求解线性多核(liblinear)的L2惩罚项上。当样本数量>样本特征的时候，dual通常设置为False。

### 6. tol 迭代收敛标准
float类型，默认为1e-4，停止求解的标准。

### 7. fit_intercept 是否存在截距或偏差
bool类型，默认为True。

### 8. intercept_scaling
仅在正则化项为”liblinear”，且fit_intercept设置为True时有用。float类型，默认为1。

### 9. random_state 随机种子
int类型，可选参数，默认为无，仅在正则化优化算法为"sag"，“liblinear"时有用。

### 10. max_iter 算法收敛最大迭代次数
int类型，默认为10。仅在正则化优化算法为"newton-cg”, "sag"和"lbfgs"才有用，算法收敛的最大迭代次数。

### 11. verbose 日志冗余度
int类型。默认为0，就是不输出训练过程；1的时候偶尔输出结果；大于1，对于每个子模型都输出。

### 12. warm_start 热启动参数
bool类型，默认为False。如果为True，则下一次训练是以追加树的形式进行（重新使用上一次的调用作为初始化）。

### 13. n_jobs 并行数
int类型，默认为1。1的时候，用CPU的一个内核运行程序；2的时候，用CPU的2个内核运行程序；为-1的时候，用所有CPU的内核运行程序。

