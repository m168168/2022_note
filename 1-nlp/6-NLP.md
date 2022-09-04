# 6-NLP

微服务基本介绍

入侵性小

稳定性高

功能强大 

docker  kuberbets istio

kafaka actor

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210518101655098.png" alt="image-20210518101655098" style="zoom:50%;" />

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210518101729826.png" alt="image-20210518101729826" style="zoom:50%;" />

LossFuction:

连续变量：   L2 (y_pre,y_real) = (y_pre - y_rel)2

​                    L1 = |y_pre - y_rel|

CrossEntrop:

Dense:

drouout:

batch_Normalization:

embedding:

word Embedding : 无标注的数据

马尔科夫过程

![image-20210518105330490](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210518105330490.png)

隐马尔可夫过程

![image-20210518105315900](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210518105315900.png)

CNN :  局部特征提取器

feature kenel :   降维

池化 ： average pool  , max pool 





## 2： 数据挖掘

![image-20210521092408689](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210521092408689.png)

![image-20210521092445715](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210521092445715.png)

![image-20210521092508005](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210521092508005.png)

![image-20210521092538060](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210521092538060.png)

## Target Meaning

![image-20210521093324515](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210521093324515.png)

Onehot  Encoding 

Ordiany Encoding  

Entity Embedding :

### 1：CDF: 累计分布概率

$$
 p(X<=x) =F_x(x) 
$$

Box-Cox  变换

Yeo-Johson 变换

AutoCross

### 降维的方法：

为什么要降维：

找到宏观信息

找到交叉效应

不建议先降维再拟合模型

找到隐藏变量  变量与变量之间的关系

PCA：

NMF： 

TSNE:  KL 距离

![image-20210521110514581](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210521110514581.png)

Denosing AutoEncoder:(加噪声)   DAE

Variational Encoder  变分贝叶斯





