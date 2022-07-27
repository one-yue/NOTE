# SVM

## 分类：

### 1. LinearSVC 线性支持向量分类

与使用SVC分类器设置参数（kernel='linear'）类似，不过是用liblinear实现而非libsvm，在惩罚函数和损失函数上有更大的灵活性

针对大样本能够实现交款的运算效果和较好的结果

### 2. NuSVC

和SVC基本类似，但是需要通过参数控制向量机的个数

参数：

1. C float，default=1.0 

    取值在0-1之间，C越大代表这个分类器对边界内噪声点的容忍度越小，分类准确率高，但是容易过拟合，泛化能力擦汗

2. kernel enum, default='rbf' 

    取值：
    ```python
    {'linear', 'poly', 'rbf', 'sigmoid', 'precomputed'}
    ```
    核函数类型，默认是高斯核函数

3. degree int, default=3 

    多项式核的阶数，当kernel='poly'，此参数才有用

4. gamma default='scale'

    取值：
    ```python
    {'scale', 'auto'} or float 
    ```

    核函数系数，当核函数为'rbf','poly','sigmoid'，此系数才起作用
    
    - gamma='scale'，计算方式为：1 / (n_features * X.var()) 
    - gamma='auto', 计算方式为：1 / n_features

5. coef0 float, default=0.0

    核函数的常数项，只对'poly','sigmoid'有用

6. shrinking boolean, default=true

    是否使用启用启发式收缩方式。启发式收缩方式就是：如果能预知哪些变量对应着支持向量，则只要在这些样本上训练就够了，其他样本可不予考虑，这不影响训练结果，但降低了问题的规模并有助于迅速求解，起到一个加速训练的效果。

7. probability boolean, default=true

    是否启用概率估计。这必须在调用fit之前启用，这将减慢该方法的速度，因为它在内部使用5倍交叉验证，并且predict\u proba可能与predict不一致。注意，预测时应用clf.predict_proba

8. tol float, default=0.001

    停止训练的误差精度

9. class_weight

    默认为None,给每个类别分别设置不同的惩罚参数C，如果没有给，则会给所有类别都给C=1，即前面指出的参数C. 

10 max_iter int, default=-1

    最大迭代次数，如果为-1，表示不限制

11 decison_function_shape 

    取值：
    ```python
    {'ovo','ovr'}
    ```

12 break_ties boolean, default=false

    如果为true，decision_function_shape='ovr'，并且类数>2，则根据decision_function的置信值预测将打破联系；否则，将返回绑定类中的第一个类。请注意，与简单预测相比，打破联系的计算成本相对较高。

13 random_state int, default=None

    控制伪随机数的生成，以洗牌数据进行概率估计。当概率为假时忽略。在多个函数调用之间传递int以获得可再现的输出。

### 3. SVC

基于libsvm实现的，大样本很难收敛

## 回归：

### 1. LinearSVR

### 2. NuSVR

### 3. SVR