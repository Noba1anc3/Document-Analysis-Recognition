## 启发
1. 在文档信息抽取任务当中加入远程监督，反馈式训练的概念
2. 信息抽取之于NLP相当于NER或Slot Filling，之于CV相当于目标检测
3. Hungarian算法

ICDAR 2017  Technical University of Denmark

## Introduction
CloudScan能够学习一个通用的模型。  
CloudScan：一个简单，免于配置和维护的较高准确率的发票分析系统，既可以分析见过的模板，也可以分析没见过的模板。其内没有模板的概念，它不依赖于任何系统集成和先验知识，同时是第一个可以精确地分析没见过的发票模板的发票分析系统，它的自动化训练数据提取与远程监督的思想十分接近。

我们的工作可以被看成是一个命名实体识别系统，也可以被看成是一个slot filling的系统。  
无论是NER还是SLot Filling，一个通用的方法是对每一个token分类其属于哪个实体或哪个slot

## CloudScan
### Overview
CloudScan引擎包含六个步骤：
1. 文本提取（检测+识别） 处理成hOCR的格式
2. 为每一行创建一个单词的N-grams
3. 为每个N-gram计算特征
4. 对每个N-gram特征向量进行分类
5. 决定输出文档当中每个field应该属于哪一个N-grams。对于每一个field，都使用基于正则表达式的语法分析器来过滤不符合field的语法的N-gram.对于与其他field没有语义联系的fields，作者使用了Hungarian算法，Hungarian算法解决的是为N个主体分配M个任务的问题。其中每个主体最多被分配一个任务，每个任务都会被分配给一个主体。为每个分配设定一个代价，Hungarian算法可以找到最小化总代价的最优分配方法。在我们的任务中，1-N-gram属于一个field的概率作为其代价。其输出是从field到N-gram的mapping
6. 基于找到对应N-gram的fields来输出一个UBL发票，UBL是基于XML的发票文件格式

### 从端用户提供的反馈来提取训练数据
UBL Invoice和PDF一同通过GUI提供给用户，用户可以修正结果当中的任何field。一旦用户修改了任何错误并接受了产出的Invoice，结果UBL会被加入到系统的数据库当中。  
分类器利用N-grams和它们的标签来训练。对于UBL文档当中每一个field，我们考虑所有的N-grams，并检查解析后的文字内容是否和field匹配。

![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqV5iq7kvS32PyDLOPF79q*R0hFA9xLQse2fCXqgCuDQBK9P5foeqndaGB9MTyjexTBq00QagXhhcx.ankitIMMs!/b&bo=ZQLuAWUC7gEDCSw!&rf=viewer_4)

通过这样的方式，GUI可以专注于使用户审查和纠正错误。这个系统相比于机器学习需要，更多的专注于用户体验。

## 实验
作者设计了两个实验，第一个实验测试在下一张发票上的表现，第二个实验是测试在没有见过的模板的下一张发票上的表现。对于第一个任务，作者把所有发票按照7:1:2的比例划分为训练集，验证集和测试集。对于第二个任务，作者把所有的发送方按照7：1：2的比例划分为训练集，验证集和测试集，这确保了三个集合当中没有共享的模板。  
作者通过比对生成的和用于验证的UBL来衡量系统的总体表现。这种衡量方式会惩罚来自不同源头的错误，例如OCR错误和验证UBL与PDF本身的不一致都会被认定为错误的预测。

### Baseline
Baseline使用逻辑回归。  
**为了得到一些上下文，我们把特征向量与上下左右方向最近的N-grams拼接在一起 （与利用lightbgm进行特征工程的实验是一样的思路）**  
逻辑回归使用SGD训练了10个Epoch。  
Baseline是Kaggle竞赛Tradeshift-text-classification的冠军方案

### LSTM
使用RNN的理由
- 上下文对于分类每一个N-gram十分重要，然而在逻辑回归当中每个N-gram都是一个孤岛，这使我们需要利用特征工程来capture上下文
- RNN以一种条理化的方式把整个invoice考虑进来，它免除了我们为了capture上下文所特意去做的特征工程

RNN的输出有65个个逻辑单元，其中32个类可以是Begining或者是Inside，除此之外还有output。
