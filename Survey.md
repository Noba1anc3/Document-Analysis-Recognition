## 文档理解

![1596418728900](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596418728900.png)

![1596418889611](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596418889611.png)

![1596418903848](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596418903848.png)



## 1.文档语义分割

### 语义分割的定义

​		语义分割是当今计算机视觉领域的关键问题之一。从宏观上看，语义分割是一项高层次任务，为实现场景的完整理解铺平了道路。场景理解作为一个核心计算机视觉问题，其重要性在于越来越多的应用程序通过从图像中推断知识来提供营养。其中一些应用包括自动驾驶，人机交互，虚拟现实等。 其涉及将一些原始数据（例如，平面图像）作为输入并将它们转换为具有突出显示的感兴趣区域的掩模。许多人使用术语全像素语义分割（full-pixel semantic segmentation），其中图像中的每个像素根据其所属的感兴趣对象被分配类别。 

### 文档语义分割的定义

​		文档语义分割在学术上尚且没有一个统一的定义，但总体而言都是在解决同一个问题，即在文档图像上的语义分割任务。进一步地，文档语义分割可以分类为OCR前的语义分割和OCR后的语义分割，在此选取两篇论文中的定义来阐述。

![1596420457262](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596420457262.png)

![1596420468285](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596420468285.png)

#### OCR前语义分割

​		对于OCR前的语义分割，Bukhari 等人在 DAS 2010 中发表的论文的表述如下 : “文档图像的语义分割将文档分割为文字和非文字区域，是文档图像分析任务中提升OCR结果的一个十分重要的预处理步骤”。也就是说，OCR前的语义分割通常将文档图像分割为文字，图片和表格区域。对于分割出的文字部分，可利用相关算法进行文字检测和识别。对于分割出的图片部分，可使用图像分析算法进行解析。对于分割出的表格部分，可使用表格理解算法进行表格理解。

![1596427227229](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596427227229.png)

#### OCR后语义分割

​		对于OCR后的语义分割，通常又被称作文档信息抽取，文档版面分析和文档语义结构提取。Yang 等人在 CVPR 2017 中发表的论文的表述如下 : "我们将文档语义结构提取看作一个逐像素的语义分割任务，并提出了一个统一的模型，该模型不同于传统的版面分割任务，仅仅基于视觉来分类像素"。换言之，OCR后的语义分割任务更多的融合了文字的语义信息和上下文信息，可以更好的找到更详尽的语义类型，用于文档的版面分析于信息抽取当中。

![1596436426620](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596436426620.png)

![1596436467871](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596436467871.png)

### 文档语义结构提取（Document Semantic Structure Extraction）

​	文档语义结构提取致力于理解文档图像，其目标是将文档图像分割为感兴趣的区域，并识别每个区域的属性。它通常由两个步骤完成，第一步叫做版面分割（Page Segmentation）。文档分割基于视觉，致力于将文字，图片，表格和线条等区域区分开。第二步叫做逻辑结构分析（Logical Structure Analysis）。逻辑结构分析基于语义，把每个区域分类为语义相关的类别，诸如段落，标题，字幕，列表等。

#### 版面分割

​	版面分割从大类来分有三种方法：基于规则的方法，基于机器学习的方法和基于深度学习的方法。

​	基于机器学习的方法通常由两种做法：自底向上和自顶向下。自底向上的做法首先基于局部特征（黑/白像素或连通分量）来检测单词，而后连续的将单词组成文字行和段落。然而，这样的方法常受限于鉴别结果，并且组合连通分量是十分耗时的。自顶向下的方法迭代地将文档分成列，块，文字行以及单词。使用这些方法无法很好的分割复杂版面的文档。

​	基于深度学习的方法通常使用全卷积网络（Fully Convolutional Network）来进行版面分割。然而，这些方法十分受限于视觉线索，并不能利用文字的语义信息。

#### 逻辑结构分析

​	逻辑结构被定义为文档逻辑成分的层次结构，诸如段落，列表，标题等。早期的工作使用一系列基于位置，字体和文字的启发式规则。Shilman等人将文档版面建模为语法，并使用机器学习的方法最小化非法解析的代价。Luong等人提出基于索然规则使用条件随机场对每个句子进行联合标签。然而，这些方法的效果都受限于对手工设计的特征的依赖。

## 2.基于自然语言处理的语义分割

​		基于自然语言处理的语义分割从属于后OCR的语义分割，其基本思想是将文字识别的结果转化为对应的词嵌入。通过命名实体识别（Named Entity Recognition）或槽填充的方法（Slot Filling）实现对文字区域的细分类。

​		此时，命名实体的范畴不再是人名，地名，公司名等传统NER当中定义的命名实体，而是与下游任务紧密关联的命名实体。诸如，身份证当中的命名实体是姓名，出生日期，住址，证件有效期等信息。而对于海关报关票据而言则应当是包含有：发送方，接收方，物品名称，物品单价，物品总量等信息。相对应的，以上提及的命名实体在槽填充当中则转变为需要被填充的槽。

### CloudScan - 基于循环神经网络的免配置发票分析系统 @ ICDAR 2018

​		CloudScan是一个简单的，免于配置和维护的发票分析系统。其既可以分析见过的模板，也可以分析尚未见过的模板。在该系统当中并没有模板的概念，也不依赖于任何系统集成和先验知识。该方法是学术界第一个可以精确地分析没有见过的模板的发票分析系统，其自动化训练数据的提取思想与远程监督的思想十分接近。

![1596438136989](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596438136989.png)

​		该系统的引擎包含以下六个工作步骤：

​		①进行文本提取，将结果组织成hOCR格式。

​		②为每个文字行闯将一个单词级N-grams。

​		③为每个N-gram计算其特征

​		④对每个N-gram特征向量进行分类

​		⑤决定输出文档当中的每个Field应当属于哪一个N-gram。

​		⑥基于找到对应N-gram的Fields来输出一个UBL Invoice. UNL是基于XML的发票文件格式。

​		UBL Invoice和 PDF 一同通过GUI提供给用户，用户可以修正结果当中的任何Field。一旦用户修改了任何错误并接受了产出的Invoice，结果UBL 会被加入到系统的数据库当中。分类器利用N-grams和它们的标签来训练。对UBL文档当中每个field，作者考虑所有的N-grams，并检查解析后的文字内容是否和field匹配。通过这样的方式，GUI可以专注于使用户审查和纠正错误。这个系统相比于机器学习需要，更多的专注于用户体验。 

## 3.基于逐像素分类的语义分割

- Multi-scale Multi-task FCN for Semantic Page Segmentation and Table Detection. ICDAR, 2017.
- Learning  to Extract Semantic Structure from Documents Using Multimodal Fully Convolutional Neural Networks. CVPR, 2017.
- Fully Convolutional Neural Networks for Page Segmentation of Historical Document Images. DAS, 2018.
- Multi-task layout analysis for historical handwritten documents using Fully Convolutional Networks. IJCAL, 2018.
- Graphical object detection in document images. ICDAR, 2019.
- Semantic Structure Extraction on Deformed Documents via Fully Convolutional Networks.
- LayoutLM: Pre-training of Text and Layout for Document Image Understanding. KDD, 2020

![1596419779084](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596419779084.png)

逐像素分类的语义分割方法通常

### 基于视觉信息的方法



#### Multi-scale Multi-task FCN @ ICDAR 2017

​		在MMFCN当中，作者第一次用一个统一的深度学习框架同时解决语义分割和表格检测的任务，亦是第一次使用深度神经网络来生成实例的边界。此外，作者提出了一个新的合成文档方法，用合成文档训练出的模型在真实文档上取得了不错的结果。

​		其合成文档的生成效果如下：

![1596437866975](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596437866975.png)

​		MMFCN的网络框架分为语义分割和轮廓检测网络。语义分割网络逐像素预测其概率，轮廓检测网络则预测元素实例的边界。而后，将语义分割和轮廓检测网络输出的特征输入到条件随机场当中，以精确语义分割网络的输出。除此之外，作者基于语义分割的结果，利用了一些启发式规则来提取每个表格实例，并利用一个验证网络来降低假阳率。

![1596437921072](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596437921072.png)

​		作者提出的MMFCN是一个统一的框架，结合了深度学习模型和启发式规则来同时处理语义分割和表格检测两个任务。其中，预测类别和轮廓检测两个任务作为神经网络框架的两个分支同时训练。而对于后面的条件随机场，其一元项由语义分割网络输出的特征来定义，其成对项由色差和轮廓特征来定义。

### 融合视觉信息与语义信息的方法

#### Multimodal FCN @ CVPR 2017

​	MFCNN以端到端的方式，逐像素同时辨别其基于视觉和语义的类别。它是一个泛化的页面分割模型，可以基于语义功能对文字区域指定特定的标签以进行细粒度的识别。

​	为了在基于CNN的模型中融合文字信息，作者构建了一个文字嵌入图（Text Embedding Map），把它输送给了MFCNN。更具体地说，对每个句子计算其嵌入表示，将该嵌入映射给该语句所在区域的每一个像素点。

![1596342496828](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596342496828.png)

​	为了解决训练数据的问题，作者提出了一个有效的合成文档生成方式，并用它生成了大规模的预训练数据。进一步地，作者提出了两个无监督任务用于更好的提升模型泛化性。其中，通过重建原始图像，重建任务有助于学到更好的表征；连续性任务鼓励同一区域的像素拥有相似的表征。

#### LayoutLM @ KDD 2020



## 4.基于目标检测的语义分割

- DeepDeSRT: Deep Learning for Detection and Structure Recognition of Tables in Document Images. ICDAR, 2017
- Fast CNN-based document layout analysis. ICCV, 2017
- DeCNT: Deep deformable CNN for table detection. IEEE Access, 2018.
- Graphical object detection using Mask R-CNN ICDAR, 2019.
- Table detection using YOLO. ICDAR, 2019.

![1596419804068](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596419804068.png)

## 5.相关数据集

![1596436155245](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596436155245.png)

### Publaynet

### ICDAR-POD-2017

### UNLV

### IIIT-AR-DOC [DAS 2020]

![1596436245954](C:\Users\yi\AppData\Roaming\Typora\typora-user-images\1596436245954.png)

## 6.评价指标

### Precision - Recall - F1

### mAP

### IoU

## 7.参考文献

