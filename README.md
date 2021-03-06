## 2018年中国高校计算机大赛——大数据挑战赛

### 赛事内容

本次大赛基于脱敏和采样后的数据信息，预测未来一段时间活跃的用户。参赛队伍需要设计相应的算法进行数据分析和处理，比赛结果按照指定的评价指标使用在线评测数据进行评测和排名，得分最优者获胜。 

比赛链接：https://www.kesci.com/home/competition/5ab8c36a8643e33f5138cba4

### 代码及方案说明

1、ExtractFeatures.ipynb

提取特征的文件，在复赛中采用了3个训练窗口，间隔为7的提取方法。即：

窗口1：行为信息-6 to 9, 未来一周10 to 16

窗口2：行为信息1 to 16, 未来一周17 to 23

窗口3：行为信息8 to 23, 未来一周24 to 30

以下代码段为设置窗口的参数：

===============================================================================
```python
TRAIN_PREDICT_DAY = range(10,17)
TRAIN_REGISTER_DAT = range(1,10)
TRAIN_ACT_DAT = range(-6,10)

TEST_PREDICT_DAY = range(31,38)
TEST_REGISTER_DAT = range(1,31)
TEST_ACT_DAT = range(15,31)
```
===============================================================================



2、train.ipynb

训练模型的文件，复赛中lgb单模为0.9121，cat单模为0.9120



### 融合方案

1、不同模型加权融合或者blending；

2、不同窗口间隔组成的特征进行融合，上面提到的特征窗口间隔为7，那么间隔为4,5,6的特征也能提取出来，每种间隔单独训练模型后进行融合，权重跟间隔大小成正相关；这种融合方法在复赛中能充分利用训练数据，能提不少分。
