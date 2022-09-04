# **1：Meaning Representation in Computs**

P10

Hypernyms (is-a) relationships of wordNet 

knowledge based representation (基于规则)

corpus-based representation （基于语料）

​		Atomic symbols: one-hot reprention 

**issues**:  difficult to compute the similarity of two (sentence ,word)

**idea** : words with similar meaning often have similar neighbor

co-occurrence matrix constructed via neighbors

**neighbors** definition: full document VS windows 

full docement: word-document co-occurrence matrix gives general topics (latent semantic analysis)

**windows**: context windows for each word capture syntactic (POS) and sematic information

issues: 1:matrix size increases with vocabulary   2: hith dimensional 3:sparsity 稀疏

**idea: low dimensional word vector**

method1 : SVD   X = USV 

semantic relations : 语言联系 syntactic relation : 句法联系

issues: 1:computationally expensive2: difficult to add new words

**idea: directly learn low-dimensional word vectors**

method2 : directly learn low dimensional word vectors

learning representations by back-propagation 1986

a neural probabilistic language model 2003

nlp from scrath 2008

recent and most popular models : word2vec 2013 and glove  2014

as known as word embeddings 



outline   P11

- Language Modeling
- N-gram language Model
- Feed-Forward Neural Language Model
- Recurrent Neural Network Language Model 

**language modeling**

Goal : estimate the probability of  a word sequence  
$$
P(w_1,w_2,...w_n) \\
$$
example task : determinate (决定) whether a sequence is grammatical or makes more sense 

**N-gram language model :**

probability is **conditional** on a window of (n-1) previous words   **count**
$$
p(w_1,w_2,...w_n) = \sum_{i=1}^m P(w_i|w_1,..,w_{n-1})
$$
**issue**: some sequences may not **appear** in the training data(the phenomenon happens because we cannot collect all the possible text in the word as training data)

give some small probability -> Smoothing 

idea: estimate 
$$
P(w_i |w_{i-(n-1)},...,w_{i-1})
$$
**not from count ,but from NN prediction** 

**issue** : fixed context window for conditioning 用于条件的固定上下文窗口

**idea** : condition the neural network on all previous words and tie the weights at each time step

assumption: temporal information matters 时间信息很重要 

# 2: **Attention and Memory**

information from sensors

  ->sensory memory    attention

->working memory     encoding 

-> long-term memory  retrieval  

**problem**: very long sequence or an image

**solution**: pay attention on the **partial** input object each time

**Problem**: larger memory implies more parameters in RNN

**solution**: long-term memory increases memory size without increasing parameters

**Machine Translation**

Sequence-to-Sequence learning : both input and output are both sequences with different lengths

<END> 标识符 

RNN+ Attention 实现  

 Dot-Product Attention in Matrix A(Q,K,V) =soft(QK^T) V

Speech Recognition with Attention  语言辨识

Image captioning with attention  

video captioning 

Reading comprehension

# 3：Corpus  based representation



**atomic  symbols: one-hot  representation**

**issues** : difficult to compute the similarity 

**idea** : 	words with similar meanings often have similar neighbors

 **Neighbors :**  

1. high-dimensional spare word  vector 
2. low-dimensional dense word vector 
   1. method 1 : dimension reduction
   2. method 2 : direct learning  

## **1: window-based co-occurrence matrix** 

**issues :** 

1. matrix size increases with vocabulary
2. high dimensional
3. sparsity -> poor robustness

**idea : low dimensional word vector  降维**

SVD  矩阵分解

**issues:** 

1.  computationally expensive : o(mn^2)
2. ​	when n < m for n x m matrix 
3. difficult to add a new words 

## 2:  direct learning  word embedding  词嵌入

Word Embedding Benefit

Given an unlabeled training corpus ， produce a vector for each word that encodes its semantic information 。 these vectors are useful because： 

1. **semantic similarit**y between two words can be calculated as the cosine similarity between their corresponding word vectors
2. word vectors as **powerful features** for various supervised NLP tasks **since** the vectors contain semantic information 
3. propagate any information into them via neural networks and update during training 



**Word2Vec**

LM （language modeling） ： 开始的时候

predicting the next words given the proceeding contexts
$$
P(w_{t+1}|w_t)
$$
 Skip-Gram Model  （提升）

Goal : predict surrounding words within a window of each word
$$
P(w_{t-m},...w_{t-1},w_{t+1},...,w_{t+m}|w_t)
$$
CBOW (Continue Bags of Words ) :

Goal: predicting the target word given the surrounding words 
$$
P(w_t|w_{t-m},...w_{t-1},w_{t+1},...,w_{t+m})
$$

1. 层次softmax

2. negative sampling

   

## Comparision:

**Counter-based:**  统计的方法

LSA,LDA,PCA:

**pros:** 

1. fast training
2. efficient usage of statistics

**cons:**

1. primarily used to capture word similarity
2. disproportionate importance given to large counts

**Direct prediction ** 直接预测 深度学习

NNLM HLBL, RNN ,skipgram , cbow

**pros:**

1. generate improved performance on other tasks
2. capture complex patterns beyond word similarity

**cons:**

1. benefits mainly from large corpus 
2. inefficient usage of statistics

# 4： Glove :

Combining the benefits from both words

 idea : ratio of co-occurrence probability can encode meaning

**Goal** : use word vectors in neural net models built for subsequent tasks 

ability to also classify words accurately

incorporate any information into them other tasks 附加信息

Glove: Global Vectors for world Representation



# 5： Word Embedding Polysemy (一词多义 )issue

Issue :

multi-senses 

multi-aspects (semantic syntax )

**Intrinsic evaluation - word analogies**

word linear relationship

syntactic  句法 and semantic 语义 example questions

**Extrinsic Evaluation Subsequent Task**

# 5: Word Embedding Polysemy issue  一词多意



Words are polysemy

an apple a day ,keeps the doctor away.

smartphone companies including apple ...

However , their embeddings are not polysemy

issue : 

multi-senses  

multi-aspects (semantics ,syntax)

TagLM  pre-ELMO

paper : Semi-supervised sequence tagging with bidirectional language models

# 6-EMLO 

idea : contextualized word Embeddings 

![image-20210408164339989](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210408164339989.png)

![image-20210408164808690](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210408164808690.png)



![image-20210408170649769](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210408170649769.png)

# 7： Attention

**Representation of variable Length data**

input： word sequence ,image pixels(像素)，audio signal ,click logs

property: continuity ,temporal,importance distribution

**example:**

basic combination : average ,sum

neural combination: networks architectures should consider input domain properties

CNN （convolutional neural networks）

- easy to parallelize
- exploit local dependencies
- long-distance dependencies require many layers

RNN (Recurrent neural network): temporal information

- learning variable-length representatiaons
- **fit for** sentences and sequences of values
- sequential computation makes parallelization **difficult**
- No explicit modeling of long and short rang dependencies

- Attention:
  encoder-decoder model is important in NMT(机器翻译)
- RNNs need attention mechanism to handle long dependencies
- attention allows us to access any state

## Dot-product Attention

input: a query q and a set of key-value(k-v) pairs to an output 

output: weighted sum of values

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210330154938401.png" alt="image-20210330154938401" style="zoom:33%;" />

self-attention

Transformer 

Multi-Head Attention:
idea: allow words to interact with one another

Model: 

1. Map Q,K,V to lower dimensional spaces
2. apply attention ,concatenate outputs
3. linear transformation

![image-20210331143448880](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331143448880.png)

![image-20210331143535394](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331143535394.png)

# 8: BERT Bidirectional Encoding Representation From transformers

idea: contextualized word representations **learn word vectors** using long contexts using Transformer instead of LSTM

## **1: Masked Language Model**

idea: language understanding is bidirectional while LM  only uses left or right context

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331150331050.png" alt="image-20210331150331050" style="zoom:50%;" />

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331150402542.png" alt="image-20210331150402542" style="zoom:50%;" />



## 2: Next Sentence Prediction

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331150511383.png" alt="image-20210331150511383" style="zoom:50%;" />

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331150714384.png" alt="image-20210331150714384" style="zoom:50%;" />

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331150734082.png" alt="image-20210331150734082" style="zoom:50%;" />





# 9: Transformer-XL:(extra-long)



idea: segment-level recurrence





# 9: ERNIE : Enhanced Representation Through knowledge integration

![image-20210331150917175](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331150917175.png)

# 10:Handing Out-of-vocabulary

Typical , such words are set to the **UNK** token and are assigned the same vector ,which is an ineffective choice if the number of OOV words is large

Subword Embeddings:

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331153440412.png" alt="image-20210331153440412" style="zoom: 50%;" />

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331153508964.png" alt="image-20210331153508964" style="zoom:50%;" />![image-20210331153525045](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331153525045.png)

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331153508964.png" alt="image-20210331153508964" style="zoom:50%;" />![image-20210331153525045](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210331153525045.png)

# 11: RoBERT

Dynamic masking  动态Mask

each sequence is masked in 10 different ways over the 40 epochs if training

original masking is performed during data preprocessing 

原来的BERT是静态mask，即在数据预处理阶段把所有的数据都mask了，在训练阶段保持不变，即使在不同的epoch里。但这样显然是有问题的， 为此，在实践中我们把数据复制10份，然后统一进行mask，然后再保持不变，送入训练过程，相当于每种mask一共需要被看4次，而不是原来的40 次了。那么动态mask就是训一个mask一个，这样基本可以保证每次看到的都不一样。下面是BERT_base使用静态和动态mask的结果：

optimization hyperparameters

peak learning rate and number of warmup steps tuned separately for each setting 

setting

training is very sensitive to the Adam epsilon term

setting B2 = 0.98 imporves stability when training with large batch sizes

Data :

not randomly inject short sequences

train only with full-length sequences

original model trains with a reduced sequence length for first 90% of updates 

BooksCorpus ,CC-News OpenWebText Stories

# 12-SpanBERT:

Span masking 

a random process to mask spans of tokens

Single sentence training

a single contiguous segment of text for each training sample

Span boundary objective (SBO)

predict the entire masked span using only the spans's boundary

这篇论文的主要贡献有三：

1. 提出了**更好的 Span Mask 方案**，也再次展示了随机遮盖连续一段字要比随机遮盖掉分散字好；
2. 通过**加入 Span Boundary Objective (SBO) 训练目标**，增强了 BERT 的性能，特别在一些与 Span 相关的任务，如抽取式问答；
3. 用实验获得了和 XLNet 类似的结果，发现**不加入 Next Sentence Prediction (NSP) 任务，直接用连续一长句训练效果更好**。

**（2）加入SBO 训练目标**

Span Boundary Objective 是该论文加入的新训练目标，希望被遮盖 Span 边界的词向量，能学习到 Span 的内容。或许作者想通过这个目标，让模型在一些需要 Span 的下游任务取得更好表现。具体做法是，在训练时取 Span 前后边界的两个词，这两个词不在 Span 内，然后用这两个词向量加上 Span 中被遮盖掉词的位置向量，来预测原词。

这样做的目的是：增强了 BERT 的性能，为了让模型让模型在一些需要 Span 的下游任务取得更好表现，特别在一些与 Span 相关的任务，如抽取式问答。

# 13-XLM(Masked LM  +Translation LM)



# 14 ALBERT ALIte BERT

1: factorized embedding par

![image-20210518091843940](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210518091843940.png)

1: factorized embedding parameterization

原始的BERT模型以及各种依据transformer来搞的预训练语言模型在输入的地方我们会发现它的E是等于H的，其中E就是embedding size，H就是hidden size，也就是transformer的输入输出维度。这就会导致一个问题，当我们的hidden size提升的时候，embedding size也需要提升，这就会导致我们的embedding matrix维度的提升。所以这里作者将E和H进行了解绑，具体的操作其实就是在embedding后面加入一个矩阵进行维度变换。E是永远不变的，后面H提高了后，我们在E的后面进行一个升维操作，让E达到H的维度。这使得embedding参数的维度从O(V×H)到了O(V×E + E×H), 当E远远小于H的时候更加明显。


Cross-layer parameter sharing

跨层参数共享，就是不管12层还是24层都只用一个transformer。之前transformer的每一层参数都是独立的，包括self-attention 和全连接，这样的话当层数增加的时候，参数就会很明显的上升。之前有工作试过单独的将self-attention或者全连接进行共享，都取得了一些效果。这里作者尝试将所有的参数进行共享，这其实就导致多层的attention其实就是一层attention的叠加。


Sentence Order Prediction（SOP）

这里作者使用了一个新的loss，其实就是更改了原来BERT的一个子任务NSP, 原来NSP就是来预测下一个句子的，也就是一个句子是不是另一个句子的下一个句子。这个任务的问题出在训练数据上面，正例就是用的一个文档里面连续的两句话，但是负例使用的是不同文档里面的两句话。这就导致这个任务包含了主题预测在里面，而主题预测又要比两句话连续性的预测简单太多。新的方法使用了sentence-order prediction(SOP), 正例的构建和NSP是一样的，不过负例则是将两句话反过来。实验的结果也证明这种方式要比之前好很多。但是这个这里应该不是首创了，百度的ERNIE貌似也采用了一个这种的。

SOP 目标补偿了一部分因为 embedding 和 FFN 共享而损失的性能。Bert 原版的 NSP 目标过于简单了，它把”topic prediction”和“coherence prediction”融合了起来。SOP 对其加强，将负样本换成了同一篇文章中的两个逆序的句子，进而消除“topic prediction”。


