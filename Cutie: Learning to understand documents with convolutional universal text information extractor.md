# Cutie: Learning to understand documents with convolutional universal text information extractor

## Abstract

- Harness the effective information from both semantic meaning and spatial distribution of texts
- Apply CNN on gridded texts where texts are embedded as features with semantical connotations
- Achieving SOTA, much better than the NER based methods interms of either speed and accuracy
- Able to achieve good performance with a much smaller amount of training data

## Introduction

​		The gridded texts are formed with the proposed grid positional mapping method, where the grid is generated with the principle that is preserving texts relative spatial relationship in the original scanned document image.

![1596979650338](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596979650338.png)

## Related Work

### Rule-based

- Intellix by DocuWare requires a template being annotated with relevant fields
- SmartFix employs specifically designed configuration rules for each template
- Esser : uses a dataset of fixed key information positions for each template

Rely heavily on the **predefined template rules** to extract information from **specific invoice layouts**.

### Learning-based

#### CloudScan

- Line-based feature extraction cannot achieve best performance when texts are not perfectly aligned
- The RNN-based classifier, Bi-LSTM has limited ability to learn the relationship among distant words

#### BERT

​	Since the previous learning based methods treat the key information extraction problem as a NER problem, applying BERT can achieve a better result than the bi-LSTM in CloudScan.

## Method

