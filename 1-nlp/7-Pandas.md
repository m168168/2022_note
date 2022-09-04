# Pandas

### 1-basic grammer

```python
# 检测是否有缺失数据
df.isnull().any()
# 数据的样例
df.head()
# 重命名
df = df.rename(columns={'satisfaction_level': 'satisfaction', 
                        'last_evaluation': 'evaluation',
                        'number_project': 'projectCount' })
# 将预测标签‘是否离职’放在第一列
front = df['turnover']
df.drop(labels=['turnover'], axis=1, inplace = True)  #删除列
df.insert(0, 'turnover', front)  #插入列
df.shape
df.dtypes
## 数据统计分析
# 离职率
_rate = df.column_name.value_counts() / len(df)
# 显示统计数据
df.describe()
# 分组的平均数据统计
turnover_Summary = df.groupby('turnover')
turnover_Summary.mean()
```

### 2 basic grammer

```python
##  相关性分析
**正相关的特征:** 
**负相关的特征:**
**思考:**
- 什么特征的影响最大?
- 什么特征之间相关性最大?
# 相关性矩阵
corr = df.corr()
sns.heatmap(corr, 
            xticklabels=corr.columns.values,  # 列的名字
            yticklabels=corr.columns.values)

corr
## 进行 T-Test
***
import scipy.stats as stats
# 满意度的t-Test
stats.ttest_1samp(a = df[df['turnover']==1]['satisfaction'], # 离职员工的满意度样本
                  popmean = emp_population)  # 未离职员工的满意度均值
LQ = stats.t.ppf(0.025,degree_freedom)  # 95%致信区间的左边界
RQ = stats.t.ppf(0.975,degree_freedom)  # 95%致信区间的右边界    
# 工作评价的概率密度函数估计
fig = plt.figure(figsize=(15,4),)
ax=sns.kdeplot(df.loc[(df['turnover'] == 0),'evaluation'] , color='b',shade=True,label='no turnover')
ax=sns.kdeplot(df.loc[(df['turnover'] == 1),'evaluation'] , color='r',shade=True, label='turnover')
ax.set(xlabel='工作评价', ylabel='频率')
plt.title('工作评价的概率密度函数 - 离职 V.S. 未离职')

```

### 3-basic grammer

```python
# 将string类型转换为整数类型
df["department"] = df["department"].astype('category').cat.codes
df["salary"] = df["salary"].astype('category').cat.codes

```

## 4-basic grammer

```
pip install graphviz
ppydotplus
```

