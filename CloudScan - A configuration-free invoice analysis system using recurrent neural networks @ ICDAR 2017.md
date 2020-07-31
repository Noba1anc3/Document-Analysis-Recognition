ICDAR 2017  Technical University of Denmark

## Introduction
CloudScan能够学习一个通用的模型。  
CloudScan：一个简单，免于配置和维护的较高准确率的发票分析系统，既可以分析见过的模板，也可以分析没见过的模板。其内没有模板的概念，它不依赖于任何系统集成和先验知识，同时是第一个可以精确地分析没见过的发票模板的发票分析系统，它的自动化训练数据提取于远程监督的思想十分接近。

我们的工作可以被看成是一个命名实体识别系统，也可以被看成是一个slot filling的系统。  
无论是NER还是SLot Filling，一个通用的方法是对每一个token分类其属于哪个实体或哪个slot

## CloudScan
### Overview
CloudScan引擎包含六个步骤：
1. 文本提取（检测+识别） 处理成hOCR的格式
2. 为每一行创建一个单词的N-grams
3. 为每个N-gram计算特征
4. 对每个N-gram特征向量进行分类
5. 决定输出文档当中每个field应该属于哪一个N-grams。对于每一个field，都使用基于正则表达式的语法分析器来过滤不符合field的语法的N-gram.对于于其他field没有语义联系的fields，作者使用了Hungarian算法，Hungarian算法解决的是为N个主体分配M个任务的问题。其中每个主体最多被分配一个任务，每个任务都会被分配给一个主体。为每个分配设定一个代价，Hungarian算法可以找到最小化总代价的最优分配方法。在我们的任务中，1-N-gram属于一个field的概率作为其代价。其输出是从field到N-gram的mapping
6. 基于找到对应N-gram的fields来输出一个UBL发票，UBL是基于XML的发票文件格式

### 从端用户提供的反馈来提取训练数据
