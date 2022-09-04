京东nlp训练营

basic risk

- token
- pos 词性标注
- ner
- synatatic analysis 句法分析
- sematic analysis  语义分析

## 分词 word segmentation

前向最大匹配算法

后向最大匹配算法

## 词性标注 pos tagging 

序列标注任务

每个单词单独去做分类

对于当前单词以及上下文单词(sliding window) 去提取特征，并用这些特征去做分类

利用概率来表示序列

考虑单词之间的前后依赖关系

常见的算法：

- 隐马尔科夫模型（Hidden Markon Model) 生成模型
- 条件随机场（Conditional Random Fields）判别模型
- 最大熵 （Max Entropy）
- LSTM  + CRF
- BERT + BILstm + CRF

## 命名实体识别 Named entity Recongnitiaon





## 句法分析 Synatic Analysis

对一个句子的词语句法做分词， 比如主谓宾

S VP  V

依存语法  Depend parse

## 语义理解 Semantic Analysis

主要问题：

- 1. 如何理解一个单词的意识
- 1. 如何理解一个文本的意识

主要技术：

SkipGram ,Cbow ,Glove ,Elmo,BERT ,ALBERT ，XLNet ,Gpt-2,gpt-3 ,Tiny-BERT

常见的应用场景：

- 1. 写作助手

  2. 文本分类（情感分析， sentiment analys ， 情绪分析  emotion analysic , 主题分类  topic classification）

  3. 信息检索 infomation retrieval 

  4. 问答系统 QA （直接返回答案）

     问题类型  Factoid QA  who /what/when /where

     问题的定义

- 5 自动生成文本摘要 （Text summary）

1. extractive method 
2. abstractive method 

6 机器翻译 machine traslate 

- Rule-based method 语法树
- statistical method

7 信息抽取 

ner 识别

关系抽取

## NLP 技术栈

![image-20210607100138602](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607100138602.png)



![image-20210601210129479](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210601210129479.png)

![image-20210601212650814](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210601212650814.png)

![image-20210601212806301](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210601212806301.png)

NLG :

![image-20210607095335335](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607095335335.png)

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607095451681.png" alt="image-20210607095451681" style="zoom: 33%;" />

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607095532032.png" alt="image-20210607095532032" style="zoom:50%;" />

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607095840604.png" alt="image-20210607095840604" style="zoom:50%;" />

拼写检查： split correction

用户输出； input

候选： candidates

编辑距离：edit distance

 ![image-20210607103512692](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607103512692.png)

 过滤： 

n-gram  朴素贝叶斯



## 论文检索：

google 学术

Google Scholar:

  按作者搜索：  author: "name "

​							source: "nature"

​							allintitle: "question answer"  //在标题中出现

​							and or   

1.  survey 
2. review 
3. tutorial  

DBLP：  https://dblp.uni-trier.de 

微软学术：  https://academic.microsoft.com/home

中文检索库：

万方

维普

知网

https://www.ccf.org.cn/xspj/rgzn

ACL , EMNLP COLING NAACL

arXiv.org

机器之心 ， AI科技评论 ， PaperWeekly , DeepTech ,新智元

![image-20210607101952257](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607101952257.png)

走进一个新的领域：

关键词 ， 关键技术， 重要论文列表 ，领域划分， 领域大牛

综述， 优秀的学位论文

abstract introduction

![image-20210607102345344](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607102345344.png)

快速阅读：

abstract 

introduction

cs方向：  problem-Driven （对前人工作的优化）

![image-20210607102557408](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607102557408.png)

## 分类与特征工程：

语言模型：（一句话语法上是否通顺）

过滤词 ，停用词 ， 出现频率很低的词

word Representation

sentence Representation

Sentence Similarity

one-hot  :  Sparsity  稀疏

TF-idf Representaion

​	Distributed Representation （vector）

Learn Word Embeddings:

Model:

传统：  skipGram , Glove , CBow

考虑上下文： ELmo , BERT , XLNet

27:

![image-20210607105704651](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607105704651.png)

![image-20210607105731076](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607105731076.png)

![image-20210607110514863](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210607110514863.png)

bert源码阅读：

http://fancyerii.github.io/2019/o3/o9/bert-codes/



![image-20210608095926012](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608095926012.png)

## 方差 ，偏差

![image-20210608101446770](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608101446770.png)

![image-20210608101559026](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608101559026.png)

![image-20210608101616102](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608101616102.png)

![image-20210608101640382](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608101640382.png)

减少可避免偏差：

![image-20210608101756411](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608101756411.png)

![image-20210608101819564](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608101819564.png)

![image-20210608101859986](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608101859986.png)

参考资料：

Machine Learning Yearing

![image-20210608102357803](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608102357803.png)

## 数据不平衡：

常见的处理方法：

欠采样

过采样

模型算法：  MetaCost , Focal Loss

评价指标：

ROC- Curve  PR-Curve

NLP 数据增强：  UDA ， EDA

![image-20210608104317581](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608104317581.png)

![image-20210608104526126](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608104526126.png)

![image-20210608104628677](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608104628677.png)

![image-20210608104644064](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608104644064.png)

![image-20210608104713141](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608104713141.png)

![image-20210608104922809](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608104922809.png)

![image-20210608105004785](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608105004785.png)

![image-20210608105038209](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608105038209.png)

![image-20210608105148379](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608105148379.png)

![image-20210608105258258](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608105258258.png)

![image-20210608105645269](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608105645269.png)

![image-20210608105753738](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608105753738.png)

![image-20210608110038685](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110038685.png)

## 评价指标：

![image-20210608110210280](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110210280.png)

![image-20210608110226781](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110226781.png)





![image-20210608110145750](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110145750.png)

![image-20210608110248579](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110248579.png)

![image-20210608110444598](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110444598.png)

![image-20210608110542682](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110542682.png)

![image-20210608110608821](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110608821.png)

![image-20210608110759486](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110759486.png)

![image-20210608110823106](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110823106.png)

![image-20210608110842318](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210608110842318.png)

paper:  

推荐排序

<<Real-time personlization using Embedding for search Ranking at Airbnd>>

## CNN ：

LeNet5 :

AlexNet:

1. 更深的网络
2. 数据增广
3. ReLU
4. dropout
5. 对GPU训练

![image-20210609101846992](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609101846992.png)

CNN在文本上的应用：

关键词：  关键短语，  -》 局部性

关键信息可在不同的位置出现 -》 平移性

适当去除一些文字内容不影响语义理解， 可缩性

![image-20210609102901467](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609102901467.png)

![image-20210609102916992](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609102916992.png)

## 多模态：

MultiModal Machine Learing (MMML):

多模态表示学习  Representation

模态转化 Translation

对齐：  Alignment

多模态融合：  Fusion

协同学习：  Co-learning



![image-20210609104647608](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609104647608.png)

![image-20210609104719752](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609104719752.png)

![image-20210609104744097](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609104744097.png)

![image-20210609104807316](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609104807316.png)

![image-20210609104840560](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609104840560.png)

![image-20210609104855714](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609104855714.png)

![image-20210609104909805](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609104909805.png)

![image-20210609104927517](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609104927517.png)

![image-20210609104953058](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609104953058.png)

![image-20210609105022628](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210609105022628.png)

常见CNN：

## CPU GPU 区别：

![image-20210614093746660](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210614093746660.png)

![image-20210614093918746](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210614093918746.png)

什么类型的程序适合在GPU上运行

- 计算密集型
- 易于并行的程序

GPU 的参数：

nvidia-smi

![image-20210614095456553](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210614095456553.png)

![image-20210614095644459](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210614095644459.png)

![image-20210614095900472](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210614095900472.png)

## NER:

LTP:

Spacy:

Standford NER 

