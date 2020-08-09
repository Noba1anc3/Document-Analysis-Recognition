# DocBank: A Benchmark Dataset for Document Layout Analysis

## Abstract

​		DocBank is a benchmark dataset with **fine-grained** **token-level** annotations for document layout analysis.  

​		**Weak supervision** from the LATEX document available on the arXiv.com.

## Introduction

​		Document layout analysis can transform **semi-structured** information into a **structured** representation, meanwhile extracting key information from the documents.  

![1596957236920](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEJaEHxs6Z*ePoKGCrFXw64EltwdbQZFDsYloYn2bdJ4q3JZCkX2bcfPljT.0bOpF0cI3zFd8SgN1RpP4*PtmLrg!/r)

​		Nowadays, the sota computer vision and NLP models are often built upon the pre-trained models followed by fine-tuning on specific downstream tasks. However, pre-trained models not only require **large-scale unlabeled data** for **self-supervised learning**, but also need **high quality labeled data** for **task-specific fine-tuning** to achieve good performance.

​		Digital-born documents such as the PDFs of research papers that are compiled by LATEX using their source code. The LATEX system contains the explicit semantic structure information using **mark-up tags** as the building blocks.  

​		The advantage of DocBank is that, it can be used in any **sequence labeling models** from the NLP perspective. Meanwhile, can also be easily converted into image-based annotations to support **object detection** models in computer vision.  

## Task Definition

​		The document layout analysis task is to extract the pre-defined semantic units in VRDs.

## DocBank

​		The current DocBank totally includes 5253 documents, where the training set includes 5053 documents and both the validation set and the test set include 100 documents.

![1596957203402](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEDqgJHwgeYQbGI2kBf3QQOlolrEUWOqeCIvdbm*d82OMxoukaiA3QisZ6rpbRtb7FvfkZu*d5clyOqbd3bHlrXA!/r)

### Document Acquisition

​		Download the PDF files and the LATEX source files on arXiv.com, focus on English documents in this work.

### Semantic Structure Detection

​		DocBank is a natural extension of the TableBank.  

​		The following semantic structures are annotated in DocBank: {Title, Author, Abstract, Paragraph, Caption, Equation, Footnote, List, Section, Table, Figure and Reference}.  

​		In TableBank, the tables are labeled with the help of the **'fcolorbox'** command.  

​		Basically, there are **two types of commands** to represent semantic structures. Some of the LATEX commands are **simple words preceded by a backslash**.

<center> \section {The title of this section} </center>

​		Other commands often **start an environment**. The command ```\begin{itemize}``` starts an environment while the command ```\end{itemize}``` ends that environment.

<center>
    \begin{itemize} <br>
    	\item First item <br>
    	\item Second item <br>
    \end{itemize}
</center>

### Token Annotation

​		We use **PDFPlumber**, a PDF parser built on **PDFMiner**, to extract text lines and non-text elements with their bounding boxes.  

​		The RGB values of characters and the non-text elements can be extracted by **PDFPlumber** from the PDF files. Mostly, a token is composed of characters with the same color. Otherwise, we use the color of the first character as the color of the token.  

### Post-processing

​		In certain cases, some tokens may have multiple colors naturally and cannot be converted by the 'color' command, such as hyperlinks and references in PDF files.  

​		Generally, tokens with the same semantic structure will be organized together in the reading order. Therefore, successive tokens often have the same label within the same semantic structure. When the semantic structure alternates, the labels of adjacent tokens at the boundary will be inconsistent.

## Method

### LayoutLM

![1596963736056](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEHWzFbOJf62co*luW1QLjSnhUlFR0ohmhPplnr2aS31aDMIsnJ8Z22ye8OjcQh2D4xXawYj19zAkfGpGscW3IRw!/r)

​		Note that we use the LayoutLM without image feature embedding because we find that the text and layout already power the pre-trained model.

### Pre-training LayoutLM

​		We choose the **Masked Visual-Language Model** as the objective when pre-training the model.

### Training Samples in Reading Order

​		We organize the DocBank using the **reading order**, which means that we sort all the text boxes and non-text elements from top to bottom by their top border positions. We tokenize all the text lines in the left-to-right order and annotate them. Basically, all the tokens are arranged **top-to-bottom and left-to-right**.

### Fine-tuning

​		We finetune the pre-trained model with the DocBank.

## Experiments

### Evaluation Metrics

​		For each kind of document semantic structure, we calculated their metrics individually.

![1596964376744](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEKUip9IqlrMicC.brjS.MRjhfiepCWONjno4euOd89vf6H3kSJdeTt2ltqOUSbMHx1nycyc3xuZMFkqj.Fyafa8!/r)

### Settings

- 8 V100 with batch=10
- 320h/epoch when training
- 1h/epoch when fine-tuning
- 12 Transformer Layers
- Hidden state size : 768
- AdamW with Initial LR : 5e-5

### Results

![1596964903583](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEJ4rxlXCYBkCrZncDXU6GgZm6eosBkQAmyfHtJRsHIfgGcvDwNFiknFzxliYhW7kfyu*8CoNM2Yd8.Ix9PK1uGw!/r)

​		As this work is still in progress, we will enlarge the DocBank dataset and update the results in the revised version later.  

## Case Study

![1596965069947](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEFIviifQdZmatelswemCFWlKqaL7eBRui73GuURE5bndMPxXV9q74yfiD0Oj0mxjRJfpdjRAe.gM9mOEfGXSKwo!/r)

​		For the pre-trained BERT model, we can see some tokens are detected incorrectly, which illustrates that only using text information is still not sufficient for document layout analysis task, and visual information should be considered as well.

## Related Work

### Rule-based

#### Bottom-up

​		Detect the connected components of black pixels as the basic computational units in document image analysis, and combining them into higher-level structures through different heuristics methods and labeling them according to different structural features.

#### Top-down

- Mask-based texture analysis, Jain and Zhong, 1996
- Run Length Smearing Algorithm, Wahl, 1982
- Document projection profile, Shafait and Breuel, 2010
- X-Y cut algorithm, Nagy and Seth, 1984

### Conventional Machine Learning

- Dynamic MLP, Baechler, 2013
- Gradient Shape Feature (GSF), Diem, 2011
- Scale Invariant Feature Transform (SIFT), Garz, 2010, 2011, 2012
- Texture Features and geometric features

### Deep Learning

- FCNN with a weight-training loss scheme, Capobianco, 2018
- Multi-task document layout analysis using CNN, Oliveira, 2018
- Pixel-by-pixel classification task, Yang, 2017

## Conclusion

​		For the future research, we will further **integrate more visual information** by using the **convolution neural network** to extract features from the document images, which will give the model more information that existing approaches might lack.
