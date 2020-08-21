# LayoutLM: Pre-training of Text and Layout for Document Image Understanding

## C
### Thinking
#### BERT Pretraining Model
During the implementation of MFCNN, I did not use the CBOW language model which used in the original paper, but used pretrained BERT for language feature extraction. However, the BERT model provided by Google is a generalized language model, which is not suitable for specific domain of Visually Rich Documents. In the previous attempt, as the dimension of feature extracted from BERT is 768, which is much more than the dimension of the image, I choose to use PCA not only for dimension reduction but also make the vectors domain related. Given the problems faced in the previous work, it is clear that a pretrained language model for VRDs is urgent not only for its more effective but also can reduce the cost for trans-domain finetune stage.

#### Idea of joint training of textual, graphical and layout information in a pretrained model
As illustrated in the paper of MFCNN, image feature is extracted by a encoder-decoder architecture, and then it combines with textual feature for prediction. However, under this situation, the image feature and textual feature is not learned in a united way, they cannot perform at its best level when combined together. Besides, during the experiments of rule-based IE and LightGBM, image feature is no longer usable, but layout information yield great importance. It is evident that these three features carry great information, thus we need to try to train a modified BERT model with the mixture of textual and layout information in a single framework. Image features are also leveraged to get higher performance.

### Engineering
### 2-D position Embedding
Based on the experience of rule-based IE and LightGBM, it is evident that layout information contributes a lot to the semantic representation.  
Like Right-Below Zone of key-value extraction and the relative positions between words.  

### Multi-label Document Classification
Based on the experience of MFCNN, it has been seen that the generalization of MFCNN is not big enough, it is essential to judge the type of invoice before use a specific model to inference on it. Therefore, it is important to capture the document-level feature for image classification.

## Abstract
Pretraining techniques have been verified successfully in a variety of NLP tasks in recent years.  
Despite the widespread use of pre-training models for NLP applications, they almost exclusively focus on  
text-level manipulation, while neglecting layout and style information that is vital for document image understanding.

LayoutLM
- Jointly model interactions between text and layout information
- Leverage image features to incorporate words' visual information into LayoutLM
- The first time that text and layout are jointly learned in a single framework for document-level pre-training
- SOTA on : form understanding, receipt understanding, document image classification

## Introduction
Document AI, or Document Intelligence, is a relatively new research topic that refers techniques for  
**automatically reading, understanding, and analyzing business documents**.

Business documents
- digital-born, occurring as electronic files
- scanned form, comes from written or printed on paper
- purchase order, financial report, business email, sales agreement, vendor contract, letter, invoice, receipt, ...

Understanding business documents is a very challenging task due to  
**the diversity of layouts and formats, poor quality of image as well as the complexity of template structures**.

Contemporary approaches for document AI are usually built upon  
deep neural networks from a cv or nlp perspective, or a combination of them.

The first to propose a table detection method for PDF documents based on CNN :  
- A Table Detection Method for PDF Documents Based on Convolutional Neural Networks. [2016IAPR Workshop on DAS]

Leveraged more advanced Faster and Mask R-CNN model :  
- DeepDeSRT: Deep Learning for Detection and Structure Recognition of Tables in Document Images. [2017 ICDAR]
- Visual Detection with Context for Document Layout Analysis. [2019 EMNLP-IJCNLP]
- PubLayNet: largest dataset ever for document layout analysis. [2019]

Take advantage of text embeddings from pre-trained NLP models :  
- Learning to Extract Semantic Structure from Documents Using Multimodal Fully Convolutional Neural Networks. [2017 CVPR]

Combine textual and visual information for information extraction :  
- Graph Convolution for Multimodal Information Extraction from Visually Rich Documents. [2019]
 
Most of these methods confront two limitations: 
1. They rely on a few human-labeled training samples without fully exploring **the possibility of using large-scale unlabeled training samples**. 
2. They usually leverage either pre-trained CV models or NLP models, but do not consider a **joint training of textual and layout information**. 

Therefore, it is important to investigate how **self-supervised pre-training of text and layout** may help in the document AI area.

Inspired by the BERT model, where input textual information is mainly represented by  
text embeddings and position embeddings, LayoutLM further adds two types of input embeddings:
1. a 2-D position embedding that denotes the relative position of a token within a document; 
2. an image embedding for scanned token images within a document.

Multi-task Learning Objective
- Masked Visual-Language Model (MVLM) loss
- Multi-label Document Classification (MDC) loss

the LayoutLM is pre-trained on the IIT-CDIP Test Collection 1.02,  
which contains more than 6 million scanned documents with 11 million scanned document images.

We select three benchmark datasets as the downstream tasks to evaluate the performance of the pre-trained LayoutLM.
- FUNSD : Spatial Layout Analysis and Form Understanding [ICDARW 2019]
- SROIE : Scanned Receipts Information Extraction
- RVL-CDIP : Document Image Classification [ICDAR 2015]

Contributions
- For the first time, textual and layout information from scanned document images is pre-trained in a single framework
- LayoutLM uses the masked visual-language model and the multi-label document classification as the training objectives
- The code and pre-trained models are publicly available at https://aka.ms/layoutlm for more downstream tasks

## LayoutLM
### BERT
The BERT model is an **attention-based bidirectional language modeling approach**.  
It has been verified that the BERT model shows effective **knowledge transfer from the self-supervised task with large-scale training data**.  
The architecture of BERT is basically a **multi-layer bidirectional Transformer encoder**.  

Given a set of tokens processed using WordPiece, the input embeddings are computed by summing the corresponding word embeddings, position embeddings, and segment embeddings. Then, these input embeddings are passed through a multi-layer bidirectional Transformer that can generate contextualized representations with an adaptive attention mechanism.  

Two steps in the BERT framework
- pre-training
- fine-tuning

Objectives to learn the language representation during pre-training
- Masked Language Modeling (MLM)
- Next Sentence Prediction (NSP)

In the fine-tuning, task-specific datasets are used to update all parameters in an end-to-end way.

### LayoutLM
When it comes to visually rich documents, there is much more information that can be encoded into the pre-trained model.  
Basically, there are two types of features which substantially improve the language representation in a visually rich document.
- Document Layout Information
- Visual Information

#### Document Layout Information
The relative positions of words in a document contribute a lot to the semantic representation.  
Embed these relative positions information as 2-D position representation.

#### Visual Information
The visual information can be represented by image features and effectively utilized in document representations.  

### Model Architecture
We use the BERT architecture as the backbone and add two new input embeddings: a 2-D position embedding and an image embedding.  

#### 2-D Position Embedding
2-D position embedding aims to model the relative spatial position in a document.  
We consider a document page as a coordinate system with the top-left origin. The bounding box can be precisely defined by (x0, y0, x1, y1). We add four position embedding layers with two embedding tables, where the embedding layers representing the same dimension share the same embedding table.

#### Image Embedding
With the bbox of each word from OCR, we split the image into several pieces, and they have a one-to-one correspondence with the words.  
We generate the image region features with these pieces of images from the Faster R-CNN as the token image embeddings.  
For the [CLS] token, we also use the Faster R-CNN model to produce embeddings using the whole scanned document image as the ROI to benefit the downstream tasks which need the representation of the [CLS] token.

### Pre-training LayoutLM
#### Masked Visual-Language Model
During the pre-training, we randomly mask some of the input tokens but keep the corresponding 2-D position embeddings, and then the model is trained to predict the masked tokens given the contexts.

#### Multi-label Document Classification
Given a set of scanned documents, we use the document tags to supervise the pre-training process so that the model can cluster the knowledge from different domains and generate better document-level representation.

#### Fine-tuning LayoutLM
The pre-trained LayoutLM model is fine-tuned on three document image understanding tasks

## Related Work
### Rule-based Approaches
The rule-based approaches contain two types of analysis methods : bottom-up and top-down
#### Bottom-up
Bottom-up methods usually detect the connected components of black pixels as the basic computational units.  
The document segmentation process is to combine them into higher-level structures through different heuristics and label them according to different structural features.

#### Top-down
Top-down methods often recursively split a page into columns, blocks, text lines and tokens.

#### Disadvantage
They require extensive human efforts to figure out better rules, while sometimes failing to generalize to documents from other sources.

### Machine Learning Approaches
- Artificial Neural Network
- SVM
- GMM

Time-consuming to design manually crafted features

### Deep Learning Approaches
Two limitations
- Rely on limited labeled data while leaving a large amount of unlabeled data unused
- leverage pre-trained CV models or NLP models, but do not consider the joint pre-training of text and layout

LayoutLM addresses these two limitations and achieves much better performance compared with the previous baselines.

## Conclusion and Future Work
### Conclusion
- Simple yet effective
- Pre-training with text and layout information in a single framework
- Based on Transformer
- Multimodal input
- Self-supervised way training

### Future work
- More data
- More computation resources
- Train LayoutLM using the LARGE architecture
- Involve image embeddings in the pre-training step
- Explore new network architectures
- Explore other self-supervised training objective
