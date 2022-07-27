# StackingClassifier

## 1. 参数

### 1. estimators list

    第一层的分裂期

### 2. final_estimator

    第二层的分类器

### 3. cv: int, cross-validation generator, iterable, or 'prefit', default=None

    用于交叉验证final_estimator训练器

### 4，stack_method 

取值:
```python
{'auto', 'predict_proba', 'decision_function', 'predict'}, default='auto'
```

    auto: 则会尝试每个方法

### 5. n_jobs: int, default=None

    处理器并行数

### 6. passthrough：bool， default=False

    如果为假，则只有估计器的预测将用作final_estimator的训练数据。如果为True，则根据预测和原始训练数据训练final_estimator。

### 7. verbose: 日志级别