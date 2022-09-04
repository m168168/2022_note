machine learning

## **决策树**

- 分类树
- 回归树

**信息熵** （用来衡量信息不确定性的指标）
$$
H(X) = - \sum_{i=1}^nP(X=i)log2P(X=i)
$$
**条件熵：** 在给定随机变量Y的条件下，随机变量X的不确定性
$$
H(X|Y=u)=-\sum_{i=1}^nP(X=i|Y=u)log2P(X=i|Y=u)
$$
**信息增益：**  熵 - 条件熵，代表在一个条件下，信息不确定性的减少程度
$$
I(X,Y)= H(X) - H(X|Y)
$$


**基尼指数**(不纯度) 表示在样本集合中一个随机选中的样本被分错的概率
$$ {r}
Gini(P) = \sum_{k=1}^Kp_k(1-p_k) = 1-\sum_{k=1}^Kp_k^2 \\
\text (其中，p_k表示选中的样本属于第k个类别的概率)
$$
Gini指数越小，表示集合中被选中的样本被分错的概率越小，集合纯度越高

当集合中所有样本为一个类别时，基尼指数为0

**回归树** regression tree

每一片叶子都输出一个预测值，预测值一般是叶子节点所含训练集元素输出的均值

回归树的分支标准： 标准方差 standard Deviation

回归树使用某一特征将原集合分为多个子集，用标准方差衡量子集的元素是否相近，越小表示越相近。

每一片叶子节点中样本预测值都是一样的（在分类问题中是一类，在回归问题是某个值）



## **集成学习**

- bagging ： 随机森林
- boosting: adaboost GBDT ,XGBoost ,LightGBM

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526094701588.png" alt="image-20210526094701588" style="zoom: 50%;" />

**Bagging (Bootstrap Aggregating)**

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526095943587.png" alt="image-20210526095943587" style="zoom: 50%;" />

n： n个学习器  

每次选择 m 个样本 组成 数据集Di ,  训练学习器 hi  ,最后取平均

![image-20210526100444365](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526100444365.png)

**Boosting** 

![image-20210526100726397](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526100726397.png)

## **随机森林 ：**

 bagging + 决策树

![image-20210526101041557](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526101041557.png)

![image-20210526101226294](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526101226294.png)

常见调参：
n_estimators:森林中决策树的个数，默认是10
criterion：度量分裂质量，信息熵或者基尼指数
max_features：特征数达到多大时进行分割
max_depth:树的最大深度
min_samples_split:分割内部节点所需的最少样本数量
bootstrap:是否采用有放回式的抽样方式
min_impurity_split：树增长停止的阀值



## Adaboost:

![image-20210526102127290](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526102127290.png)

**adaboost : 算法流程**

![image-20210526104117557](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526104117557.png)

w11 : 表示第1个分类器 ，第一个样本的权重

![image-20210526104217554](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526104217554.png)

![image-20210526104321126](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526104321126.png)

定理： 随着M的增加， AdaBoost 最终分类器G(x) 在训练集上错误率越来越小

## GBDT

提升树：Boosting Decision Tree==

提升树是以CART决策树为基学习器的集成学习方法

![image-20210526104544210](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526104544210.png)

BDT

![image-20210526104913489](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526104913489.png)

![image-20210526105117490](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526105117490.png)

![image-20210526105235200](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210526105235200.png)

**GBDT：** Gradient Boosting Decision  Tree 梯度提升树  （回归树）

https://zhuanlan.zhihu.com/p/29765582  

梯度提升+ 决策树

利用损失函数的负梯度拟合基学习器（负梯度代替残差）



![image-20210527094943547](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210527094943547.png)

![image-20210527095209176](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210527095209176.png)

GBDG 的流程 回归

![image-20210601091606845](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210601091606845.png)

GBDT： 分类

![image-20210601091814191](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210601091814191.png)

![image-20210603103847728](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603103847728.png)

## XGBoost

![image-20210603103958067](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603103958067.png)

![image-20210603104136479](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603104136479.png)

![image-20210603104245502](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603104245502.png)

![image-20210603104342446](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603104342446.png)

![image-20210603104549587](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603104549587.png)



![image-20210603104626928](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603104626928.png)

正则项：

![image-20210603104759355](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603104759355.png)

![image-20210603104833030](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603104833030.png)

![image-20210603104920814](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603104920814.png)

![image-20210603105003858](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603105003858.png)

![image-20210603105119813](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603105119813.png)

![image-20210603105421045](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603105421045.png)

![image-20210603105607555](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603105607555.png)

![image-20210603105804980](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603105804980.png)

![image-20210603110907697](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210603110907697.png)

## LightGBM：

线性回归：

计算两行之间的相关性：

np.corrcoef(y1 , y2)  # 两个都是行向量

局部加权线性回归：

Locally Weighted Linear Regression (LWLR)
$$
\hat{w} = (X^TWX)^{-1}X^TW_y \\
W 是一个矩阵，用来给每个数据点赋予权重

LWLR 使用 核函数， 常用的是高斯核 \\

w(i,i) = exp[  \frac{|x^i-x|^2}{-2k^2} ]
$$






https://blog.csdn.net/laputa_ml/article/details/80072570

![image-20210608161812598](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608161812598.png)

![](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608161905250.png)

![image-20210608161944721](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608161944721.png)

![image-20210608162007950](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608162007950.png)

## Colab 的使用：

Colab 中的可用 GPU 通常包括 Nvidia K80、T4、P4 和 P100。在任何给定时间，您都无法选择在 Colab 中连接的 GPU 类型。如果想要更稳定地使用 Colab 最快的 GPU，用户可以订阅 [Colab Pro](http://colab.research.google.com/signup?utm_source=faq&utm_medium=link&utm_campaign=what_types_of_gpus)。
