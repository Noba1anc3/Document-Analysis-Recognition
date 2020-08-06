[TOC]

## 1. 文档语义分割

### 1.1 语义分割的定义

​		语义分割是当今计算机视觉领域的关键问题之一。从宏观上看，语义分割是一项高层次任务，为实现场景的完整理解铺平了道路。场景理解作为一个核心计算机视觉问题，其重要性在于越来越多的应用程序通过从图像中推断知识来提供营养。其中一些应用包括自动驾驶，人机交互，虚拟现实等。 其涉及将一些原始数据（例如，平面图像）作为输入并将它们转换为具有突出显示的感兴趣区域的掩模。许多人使用术语全像素语义分割（full-pixel semantic segmentation），其中图像中的每个像素根据其所属的感兴趣对象被分配类别。 

### 1.2 视觉丰富文档

视觉丰富文档 (Visually Rich Documents, VRDs) 指含有丰富的视觉和布局信息的文档，如票据、保险单、营业执照等。在这类文档中，文本的语义结构不仅取决于文字本身的含义，还取决于视觉特征。如某行文本的相对于其他文本的位置、文本的字体字号、是否倾斜或加粗等。处理这类文档，不能简单地将文本序列化为一维数据，否则必然会导致文档信息的损失。如下图所示，"$649.35"表示的是"Total Amount"，不仅是因为"$649.35"本身表示的是金钱的数量，还因为其左侧的"Total"字样，两者共同决定了"$649.35"是"Total Amount"的值。

<div align="center"><img src="https://i.loli.net/2020/08/04/XqMH6fKxbZiDehU.png"  width="500"/></div>

### 1.3 文档语义分割的定义

​		文档语义分割在学术上尚且没有一个统一的定义，但总体而言都是在解决同一个问题，即在文档图像上的语义分割任务。进一步地，文档语义分割可以分类为OCR前的语义分割和OCR后的语义分割，在此选取两篇论文中的定义来阐述。

<div align="center"><img src="http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEK0sKe8cnyDZUZBs1KWk64OBd5iMFqfGlMS41sRCqxvSi2ZXXarVpNbiuOebb0RXlfjpeOghrKPQQ6J4SMSI7AI!/r" /></div>
<div align="center"><img src="http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrENGrtySjFhQ8TF5UgHj8hIqSzj8RsLRO*cCOzpvtTDRvk8Eri*I3B5siBs6QSGOpq.kkLpTmbHdi8IQQ55ir0ig!/b&bo=SQOMAEkDjAADGTw!&rf=viewer_4" /></div>

#### 1.3.1 OCR前语义分割

​		对于OCR前的语义分割，Bukhari 等人在 DAS 2010 中发表的论文的表述如下 : “文档图像的语义分割将文档分割为文字和非文字区域，是文档图像分析任务中提升OCR结果的一个十分重要的预处理步骤”。也就是说，OCR前的语义分割通常将文档图像分割为文字，图片和表格区域。对于分割出的文字部分，可利用相关算法进行文字检测和识别。对于分割出的图片部分，可使用图像分析算法进行解析。对于分割出的表格部分，可使用表格理解算法进行表格理解。

<div align="center"><img src="http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEJ61FQaImMR6n1MlTCfM8QfXVf1u99bSqcpyI9s4FOf.ByrK7EpFQoYEL0rloyUqCMwqbK3QuQJXacDyo6k8FbQ!/r"/></div>

#### 1.3.2 OCR后语义分割

​		对于OCR后的语义分割，通常又被称作文档信息抽取，文档版面分析和文档语义结构提取。Yang 等人在 CVPR 2017 中发表的论文的表述如下 : "我们将文档语义结构提取看作一个逐像素的语义分割任务，并提出了一个统一的模型，该模型不同于传统的版面分割任务，仅仅基于视觉来分类像素"。换言之，OCR后的语义分割任务更多的融合了文字的语义信息和上下文信息，可以更好的找到更详尽的语义类型，用于文档的版面分析于信息抽取当中。

![1596436426620](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEF58Y*o9EtyL*X6ehd7xV8ntlXxUBywxjc3tLfXLIyDus3tvtZ14T4dOR5kEIJRDPoEX7*49YXjINCev1phYvRE!/r )

![1596436467871](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEFMtLyATAFC70E*kNS9sWWLulUrFfd03bDi6qjuvg81lLwxkt4mqJ*ncEb2eMZasJRKydfhe*091iPLZrwwxAm0!/r )

## 2. 数据集

​		语义分割模型的训练需要庞大的训练数据，从2010年开始陆续出现了若干具有一定规模的语义分割数据集。这些数据集有些专注于表格检测的任务，有些致力于版面分割的任务，近一两年来出现了拥有更多细粒度标签的大规模语义分割数据集，诸如PubLayNet和DocBank。随着时间的推移，数据集的制作方式由人工标注转变为基于规则的弱监督生成，数据集的大小与日俱增，训练出来的语义分割模型也随之越来越强大。这使得基于大规模多领域数据集的语义分割预训练模型的设想成为现实[1]。

<div align="center"><img src="http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEOzIanVWLWA8mkhyQMEPUgvn5gKq.t7tPStAGLeHhO*UfgY1iL0uGr9yJMtCFvQr48xpDRPFq2HVwnk..0HK5hw!/r"/></div>

<div align="center"><img src="http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrELLAEF2TedUovX52*rJV3X**4ySrGDKO8llKmhOZjzshvhDUgJB6Y9YoCaYfhtg8E6heJiQjzi0Qebm30KoABHU!/r"/></div>

### 2.1 FUNSD [2]

数据集共包含199份完全标注的表单，31485个单词，9707个语义实体以及5304个关系。语义实体的类有header, question, answer, other四种。

<div align="center"><img src="https://i.loli.net/2020/08/02/RrejCufWkhZFgMQ.png"  width="700" /></div>

### 2.2 ICDAR 2013 [3]

​		该数据集是表格检测和结构识别任务中引用最多的数据集之一。它包含67个PDF，对应238页图像。其中40份来自美国政府，27份来自欧盟。在238页图像中，只有135页图像包含表，共有150个表。该数据集被广泛用于表检测和结构识别任务的算法评估。

###  2.3 ICDAR-POD-2017 [4]

​		它着重于检测文档图像中的各种图形对象（如表格、公式和图形），通过从CiteSeer的1500篇科学论文中选出的2417个文档图像来创建。它包括多种多样的页面布局—单列、双列、多列，以及对象结构的显著变化。该数据集被分成（i）由1600个图像组成的训练集，和（ii）包含817个图像的测试集。

### 2.4 SROIE [5]

该数据集出自ICDAR 2019 Robust Reading Competition的Task 3-Key Information Extraction from Scanned Receipts，训练集含626张图片，测试集含347张图片，标注的实体类有company，date，address，total四种。

<div align="center"><img src="https://i.loli.net/2020/08/03/2bLSV4OdD8Khklu.jpg"  width="400"/></div>

    {
    	"company": "STARBUCKS STORE #10208",
    	"date": "12/07/2014",
    	"address": "11302 EUCLID AVENUE, CLEVELAND, OH (216) 229-0749",
    	"total": "4.95"
    }

### 2.5 ICDAR RDCL [6]

ICDAR RDCL是文档分析与识别国际会议复杂版面文档识别竞赛的简称，每两年举办一次。比赛使用的数据集为PRImA版面分析数据集，由曼彻斯特萨福德大学PRImA实验室提出，包括当代杂志和科学文章之内的扫面页。其主要任务是进行版面分割和区域分类。

<div align="center"><img src="http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEPPOa0rFR7ADEpP546LN1rIcatM2Upr7*6JeI7GhN2aSi6nUa62sHWCQrVGfv8LfJyCJ4PbpZS.zYTcp1wKmrHQ!/r"  width="700" /></div>

### 2.6 cTDAR [7]

​		该数据集由各种格式的现代文献和存档文档组成，包括文档图像和PDF等数字格式。这些图像显示了各种各样的表格，从手工绘制的会计账簿到证券交易清单、火车时刻表、囚犯名单记录簿、印刷书籍表格、生产普查等。现代文献包括科学期刊、表格、财务报表等。注释与表区域相对应，单元格区域可用。该数据集包含（i）训练集-由600个带标注的档案和600个带表格边界框的现代注释文档图像组成，以及（ii）测试集-包括199个带注释的档案和240个带表格边框的现代文档图像。

### 2.7 DSSE-200 [8]

数据集提供了基于图片特征和语义特征的标签，包含从杂志和学术论文中获取的200个页面。页面中的区域标签有以下几种：figure, table, section, caption, list和paragraph，标注采用VOC数据集格式。图片标注示例如下图所示，其中红色表示figure，绿色表示section，蓝色表示text。

<div align="center"><img src="https://i.loli.net/2020/08/04/kJPe9w8rGabBFcy.png"  width="500"/></div>

### 2.8 Marmot [9]

​		Marmot 数据集由北京大学王选计算机研究所网络内容保护与文档处理研究室制作，它由2000页中英文组成，比例约为1 : 1。中文网页选自方正阿帕比图书馆提供的120多种不同主题的电子书，其中在每本书中选取不超过15页。英文版选自Citeseer网站1970-2011年间出版的1500多篇期刊和会议论文。页面显示了各种各样的布局—一列和两列、语言类型和表格样式。此数据集用于表格检测和结构识别任务。

### 2.9 UNLV [10]

​		它包含2889个文档图像，包括技术报告、杂志、商业信函、报纸等，其中只有427个图像包含558个表格。表区域和单元格区域的注释可用。此数据集还用于表格检测和表结构识别任务。

### 2.10 IIIT-AR-13K [11]

​		IIIT-AR-13K由印度国际信息技术学院提出，该数据集通过手工标注公开企业年报制作，一共包含13K张图片。数据集内的元素有以下五个类别：表格，图片，自然图片，LOGO和签名。这是目前最大的图像目标检测手工标注数据集。数据来源于不同语言的多家公司在若干年来发布的企业年报，这给数据集带来了很大的多样性。

### 2.11 PubLayNet [12]

​		PubLayNet是一个大型文档图像数据集，文档布局同时使用边界框和多边形进行标注。其使用的原始文档是PubMed中心开源数据集，通过自动化对齐PDF解析结果和XML文件来完成对文档的标注。该工作获得了2019年ICDAR的最佳论文奖。

![publaynet](https://i.loli.net/2020/08/04/3urWMmCeRGLxANj.png) 

### 2.12 TableBank [13]

​		TableBank是由北航与微软亚洲研究院联合提出的表格检测与识别新型数据集。该数据集是通过对网上的Word和Latex文档进行弱监督而建立的，不同于传统的弱监督数据集，作者使用的方法可以获得大规模且高质量的训练数据。其包含417,234个高质量标注表格，并且这些表格所在的文档有着各式各样的领域。

|            Task             |  Word   |  Latex  | Word+Latex |
| :-------------------------: | :-----: | :-----: | :--------: |
|       Table detection       | 163,417 | 253,817 |  417,234   |
| Table structure recognition | 56,866  | 88,597  |  145,463   |

### 2.13 DocBank [14]

​		DocBank是由北航，哈工大和微软亚洲研究院联合提出的文档版面分析数据集。与TableBank一样，同样使用弱监督的方法来建立，拥有细粒度的token级标注。该数据集使在下游任务训练的模型可以同时学习到文本的和版面的信息。目前的DocBank包含500K个文档页码，其中400K张用于训练，50K张用于验证，50K张用于测试。

![1596444872518]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEHJHm7msFudCMv2M8seHuyEONHlfeE4xZodg382PTNnuEJKg7iPYHE2kVQ34rfW4xlCDDI.Cm0EY9I.nrr.2Nuk!/r )

​		在文档版面分析任务中，已有一些基于图像的文档版面数据集，而这些数据集大多是针对计算机视觉方法构建的，很难应用于NLP方法。另外，基于图像的数据集主要包括页面图像和大型语义结构的边界框，它们不是细粒度的token级标注。此外，生成人工标记的细粒度token级文本块排列也是耗时和费力的。因此，利用弱监督以最小的努力获得细粒度的标记文档，同时使数据能够易于应用到任意的NLP和计算机视觉方法是至关重要的。

|     Dataset     | #Pages  | #Units | Image based? | Text based? | Fine-grained? | Extendable? |
| :-------------: | :-----: | :----: | :----------: | :---------: | :-----------: | :---------: |
| Article Regions |   100   |   9    |      ✔       |      ✘      |       ✔       |      ✘      |
|    GROTOAP2     | 119,334 |   22   |      ✔       |      ✘      |       ✘       |      ✘      |
|    PubLayNet    | 364,232 |   5    |      ✔       |      ✘      |       ✔       |      ✘      |
|    TableBank    | 417,234 |   1    |      ✔       |      ✘      |       ✔       |      ✔      |
|     DocBank     | 500,000 |   12   |      ✔       |      ✔      |       ✔       |      ✔      |

## 3. 评价指标

### mAP

​		mAP通常用于基于目标检测的方法，其全称是mean Average Precision。这里的Average Precision是在不同recall下计算得到的。

| Ground Truth \ Prediction |          True           |          False          |
| :-----------------------: | :---------------------: | :---------------------: |
|         **True**          | **TP (True Positive)**  | **FN (False Negative)** |
|         **False**         | **FP (False Positive)** | **TN (True Negative)**  |

​		准确率，召回率和精度的计算公式如下：

<div align="center"><img src="https://www.zhihu.com/equation?tex=P%3D%5Cfrac%7BTP%7D%7BTP%2BFP%7D%EF%BC%8C%EF%BC%88%E5%9C%A8%E9%A2%84%E6%B5%8B%E4%B8%BA%E6%AD%A3%E6%A0%B7%E6%9C%AC%E7%A7%8D%E5%AE%9E%E9%99%85%E4%B8%BA%E6%AD%A3%E6%A0%B7%E6%9C%AC%E7%9A%84%E6%A6%82%E7%8E%87%EF%BC%89"/></div>
<div align="center"><img src="https://www.zhihu.com/equation?tex=R%3D%5Cfrac%7BTP%7D%7BTP%2BFN%7D%EF%BC%8C%EF%BC%88%E5%9C%A8%E5%AE%9E%E9%99%85%E4%B8%BA%E6%AD%A3%E6%A0%B7%E6%9C%AC%E4%B8%AD%E9%A2%84%E6%B5%8B%E4%B8%BA%E6%AD%A3%E6%A0%B7%E6%9C%AC%E7%9A%84%E6%A6%82%E7%8E%87%EF%BC%89"/></div>
<div align="center"><img src="https://www.zhihu.com/equation?tex=accuracy%3D%5Cfrac%7BTP%2BTN%7D%7BTP%2BTN%2BFP%2BFN%7D%EF%BC%8C%EF%BC%88%E9%80%9A%E5%B8%B8%E7%94%A8%E5%88%B0%E7%9A%84%E5%87%86%E7%A1%AE%E7%8E%87%E7%9A%84%E8%AE%A1%E7%AE%97%E5%85%AC%E5%BC%8F%EF%BC%89"/></div>

​		Precision度量的是「查准率」，在所有检测出的正样本中是不是实际都为正样本。比如在垃圾邮件判断等场景中，要求有更高的precision，确保放到回收站的都是垃圾邮件。 

​		Recall度量的是「查全率」，所有的正样本是不是都被检测出来了。比如在肿瘤预测场景中，要求模型有更高的recall，不能放过每一个肿瘤。

​		在VOC2010以前，只需要选取当Recall >= 0, 0.1, 0.2, ..., 1共11个点时的Precision最大值，AP即为这11个Precision的平均值。在VOC2010及以后则是计算PR曲线下面积作为AP值。

​		最后，所有种类的平均AP值即为mAP值。

### Pixel-wise IoU

IoU：全称为交并比（Intersection of Union），计算的是两个矩形区域交集和并集的比值，该指标用于衡量两个矩形区域的重叠度。下图左表示交集区域，下图右表示并集区域，计算公式为：

![](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEO81hAUf4vC8RfFsAkAgImplXsKOiyQLcbhbM2LneakPXyM*lpzDw0lXENMCIvjs3lvfpYymL.VQmDRiBLhHUnc!/r)

<div align="center"><img src="https://i.loli.net/2020/08/05/6LIhKs42FC9yXUq.png"  width="500" /></div>

Pixel-wise IoU：对于语义分割任务而言，Ground Truth和Prediction都是由许多像素点组成的集合，这些像素点并不一定能刚好组成一个矩形，所有就有了基于像素点的IoU。设Ground Truth的像素点组成集合A，Prediction的像素点组成集合B，则此时计算基于像素的IoU的公式为

![](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrECsH8kB1cu1ZBKbOJ86Qo5273JqtJC.uODZ1ar.nE0kcr5n0Z7qsbYW8TTaUZc2qjXrkgtqBILh82b1YkdKKfjM!/r)

### Precision - Recall - F1

​		准确率，召回率及其对应的F1分数通常用于基于语义分割的方法，可以从像素、单词或实体三个角度计算上述指标：

<div align="center"><img src="http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqfMqTPnSmdq.h7NVm53LLRLNU1RTMelLJllRtXf9Bemt2sbIOLI69jV46ynSw6Ko2svs6vPTzJJqRaorCR00N3Q!/b&bo=*gY1Av4GNQIDCSw!&rf=viewer_4"  width="700" /></div>

- Pixel-level：
  - 对每个类别，设整张图片的所有像素点组成集合S，Ground Truth的所有像素组成集合A，Prediction的所有像素组成集合B，A∩B为TP，A-B为FN，B-A为FP，S-A-B为TN；
  - 对每个类别分别根据上述公式计算Precision，Recall和F1。

- Word-level：
  - Ground Truth中的标注格式为每个单词有一个边界框；
  - 对某个类所有Ground Truth框，若与它IoU最大的Prediction框大于某阈值，则TP个数加1，每个Prediction只负责一个Ground Truth框；
  - 在上述基础上计算Precision，Recall和F1。

- Entity-level：
  - Ground Truth中的标注格式为每个实体有一个边界框；
  - 对某个类所有Ground Truth框，若与它IoU最大的Prediction框大于某阈值，则TP个数加1，每个Prediction只负责一个Ground Truth框；
  - 在上述基础上计算Precision，Recall和F1。

### Exact Match F1 Score

上述的评估指标都是对于“关键信息定位”这一子任务而言，而非IEVRDs(Information Extraction from Virtually Rich Documents)这个整体任务。比如说mAP只是为了衡量模型提取出来的框和真实框的重叠度，并不关心后续的OCR是否能够正确提取文本。而Exact Match F1 Score旨在衡量模型处理IEVRDs这个整体任务的能力（不仅与“关键信息定位”有关，还与OCR以及诸多后处理相关）。该评测指标只关心最终的提取结果，只有当预测的文本与Ground Truth的文本完全相同时，才认为该预测结果正确。例如，提取发票中Fare字段对应的值，Ground Truth为"$4.95"，若预测值为"4.95"，认为该预测结果错误，只有当预测值刚好为"$4.95"时，才认为预测正确。

### Edit-Distance Based Accuracy

## 4. 解决方案

### 4.1 概述

​		对IEVRDs任务及其相似任务而言，其解决方案经过了以下几个发展阶段：

- 基于规则的方法
- 基于统计机器学习的方法
- 基于深度学习的方法

​		基于规则的方法通常有两种做法：自底向上和自顶向下。自底向上的做法首先基于局部特征（黑/白像素或连通分量）来检测单词，而后连续地将单词组成文字行和段落。然而这样的方法常受限于鉴别结果，并且组合连通分量十分耗时。自顶向下的方法递归地将文档分成列、块、文字行以及单词。使用这些方法无法很好的分割复杂版面的文档。同时，基于规则的方法通常依赖于固定的模板，大大降低了算法的泛化性。

​		基于机器学习的方法：人工神经网络（Artificial Neural Network）、支持向量机（Support Vector Machine）、混合高斯模型（Gaussian Mixture Model）和梯度上升决策树（Gradient Boost Decision Tree）被广泛应用于文档分析与识别并取得了显著成效。除此之外，研究人员也将文档的布局分析视为一个解析问题，并利用基于语法的损失函数来优化全局获取最优解析树。对于机器学习方法来说，它们通常需要花费大量的时间来设计手工构建的特征，并且很难获得高度抽象的上下文语义信息。此外，这些方法通常依赖于视觉线索而忽略了文本信息。

​		近年来，基于深度学习的方法逐渐取代上述两种方法称为主流，理论上，通过堆叠多层神经网络，能够拟合任意函数，且深度学习已经在多领域被证实可行。

​		起初，研究人员大都基于纯粹的图片特征或文字特征开展IEVRDs任务。例如先利用计算机视觉的相关技术（如目标检测）找到感兴趣区域，然后利用OCR技术从这些区域中提取文本；再如先利用OCR技术从文档图片提取出所有文字序列，然后利用NLP相关技术（NER等）进行信息抽取。以上两种方法的缺点在于都只考虑了部分特征，忽略了大量有用的信息。

​		实际上，对于VRDs而言，文档的语义结构不仅依赖于文字本身的含义，而且依赖于整个文档的结构和布局，想要高效地提取信息，必须将图片特征、布局特征和文字特征结合。近年来，研究人员开始尝试用不同的方法将多种特征结合，共同作用，应用于IEVRDs及其相似任务。

### 4.2 常见解决方案

|    特征构成    |                             论文                             |       时间及会议        |                数据集                 |           评估方案           |     指标      |
| :------------: | :----------------------------------------------------------: | :---------------------: | :-----------------------------------: | :--------------------------: | :-----------: |
|      图像      | **Multi-scale Multi-task FCN for Semantic Page Segmentation and Table Detection [15]** |      2017<br>ICDAR      |                                       |                              |               |
|      语义      |  **CloudScan - A configuration-free invoice analysis [16]**  |      2017<br>ICDAR      |                                       |                              |               |
|   图像+结构    | **Visual Detection with Context for Document Layout Analysis [17]** | 2019<br>EMNLP<br>IJCNLP |  Self Annotated Scientific Articles   |         mAP(IoU@0.5)         |     70.3%     |
|   图像+语义    | **Learning to Extract Semantic Structure from Documents Using Multimodal Fully Convolutional Neural Networks [18]** |      2017<br>CVPR       |              ICDAR 2015               |        Pixel-wise IoU        |    92.75%     |
|                |                                                              |                         |               SectLabel               |              F1              |    89.35%     |
|                |                                                              |                         |               DSSE-200                |        Pixel-wise IoU        |     75.9%     |
|   图像+语义    |    **Chargrid: Towards Understanding 2D Documents [19]**     |      2018<br>EMNLP      |           Private Invoices            | Edit Distance based Accuracy |    62.96%     |
|   图像+语义    | **BERTgrid: Contextualized Embedding for 2D Document Representation and Understanding [20]** |     2019<br>NeurIPS     |                                       |                              |               |
|   结构+语义    | **Cutie: Learning to understand documents with convolutional universal text information extractor [21]** |      2019<br>CVPR       |                 SROIE                 |     Strict AP / Soft AP      | 86.7% / 92.7% |
| 图像+语义+结构 | **LayoutLM: Pre-training of Text and Layout for Document Image Understanding [1]** |       2020<br>KDD       |                 FUNSD                 |     Word-level F1 Score      |    79.27%     |
|                |                                                              |                         |                 SROIE                 |     Exact Match F1 Score     |    95.24%     |
|      其他      | **Graph convolution for multimodal information extraction from visually rich documents [22]** |      2019<br>NAACL      |    Value-Added Tax Invoices (VATI)    |                              |               |
|                |                                                              |                         | International Purchase Receipts (IPR) |                              |               |

## 5. 基于自然语言处理的语义分割

​		基于自然语言处理的语义分割从属于后OCR的语义分割，其基本思想是将文字识别的结果转化为对应的词嵌入。通过命名实体识别（Named Entity Recognition）或槽填充的方法（Slot Filling）实现对文字区域的细分类。

​		此时，命名实体的范畴不再是人名，地名，公司名等传统NER当中定义的命名实体，而是与下游任务紧密关联的命名实体。诸如，身份证当中的命名实体是姓名，出生日期，住址，证件有效期等信息。而对于海关报关票据而言则应当是包含有：发送方，接收方，物品名称，物品单价，物品总量等信息。相对应的，以上提及的命名实体在槽填充当中则转变为需要被填充的槽。

### CloudScan - 基于循环神经网络的免配置发票分析系统 [16]

​		CloudScan是一个简单的，免于配置和维护的发票分析系统。其既可以分析见过的模板，也可以分析尚未见过的模板。在该系统当中并没有模板的概念，也不依赖于任何系统集成和先验知识。该方法是学术界第一个可以精确地分析没有见过的模板的发票分析系统，其自动化训练数据的提取思想与远程监督的思想十分接近。

![1596438136989](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEFORcrL0qDEv9yhfAwOTBCamKeLP6daoZkjKkuyKUrCroxpZROamhtmoXaAmHMH3xhYQPNecJYUe*izOPiPG1UU!/r)

​		该系统的引擎包含以下六个工作步骤：

​		①进行文本提取，将结果组织成hOCR格式。

​		②为每个文字行闯将一个单词级N-grams。

​		③为每个N-gram计算其特征

​		④对每个N-gram特征向量进行分类

​		⑤决定输出文档当中的每个Field应当属于哪一个N-gram。

​		⑥基于找到对应N-gram的Fields来输出一个UBL Invoice. UNL是基于XML的发票文件格式。

​		UBL Invoice和 PDF 一同通过GUI提供给用户，用户可以修正结果当中的任何Field。一旦用户修改了任何错误并接受了产出的Invoice，结果UBL 会被加入到系统的数据库当中。分类器利用N-grams和它们的标签来训练。对UBL文档当中每个field，作者考虑所有的N-grams，并检查解析后的文字内容是否和field匹配。通过这样的方式，GUI可以专注于使用户审查和纠正错误。这个系统相比于机器学习需要，更多的专注于用户体验。 

## 6. 基于逐像素分类的语义分割

### 6.1 相关文章列表

- Graphical object detection in document images. ICDAR, 2019.
- Semantic Structure Extraction on Deformed Documents via Fully Convolutional Networks.
- LayoutLM: Pre-training of Text and Layout for Document Image Understanding. KDD, 2020.
- Multi-scale Multi-task FCN for Semantic Page Segmentation and Table Detection. ICDAR, 2017.
- Fully Convolutional Neural Networks for Page Segmentation of Historical Document Images. DAS, 2018.
- Multi-task layout analysis for historical handwritten documents using Fully Convolutional Networks. IJCAL, 2018.
- Learning  to Extract Semantic Structure from Documents Using Multimodal Fully Convolutional Neural Networks. CVPR, 2017.

![1596419779084](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEGkTzgIs42v92hurpJuXmPoT7iZU.2ZyD59bsyY1ZeTncziquQQrtu6CqZ.sOWtAjFloZ2nW8s1mL28EzB8o0oc!/r)

逐像素分类的语义分割方法通常

### 6.2 基于视觉信息的方法

#### Multi-scale Multi-task FCN [15]

​		在MMFCN当中，作者第一次用一个统一的深度学习框架同时解决语义分割和表格检测的任务，亦是第一次使用深度神经网络来生成实例的边界。此外，作者提出了一个新的合成文档方法，用合成文档训练出的模型在真实文档上取得了不错的结果。

​		其合成文档的生成效果如下：

![1596437866975](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEKDjPSucZE8JONI2rMOydVxepZ6wEPN8GcufoCgAs6f.95jOVhRb1UNc5ppBDbWeeuIS9BrMysQQuIYFkcq.qhM!/r)

​		MMFCN的网络框架分为语义分割和轮廓检测网络。语义分割网络逐像素预测其概率，轮廓检测网络则预测元素实例的边界。而后，将语义分割和轮廓检测网络输出的特征输入到条件随机场当中，以精确语义分割网络的输出。除此之外，作者基于语义分割的结果，利用了一些启发式规则来提取每个表格实例，并利用一个验证网络来降低假阳率。

![1596437921072](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEBMLNilHfB7z*oMFno0HkCRD1rze3J*nkOkUbf2gUnVj6qHgMSCmxXgBzDqIRFxF8Vzfen6n7hGk78.LBluMogI!/r)

​		作者提出的MMFCN是一个统一的框架，结合了深度学习模型和启发式规则来同时处理语义分割和表格检测两个任务。其中，预测类别和轮廓检测两个任务作为神经网络框架的两个分支同时训练。而对于后面的条件随机场，其一元项由语义分割网络输出的特征来定义，其成对项由色差和轮廓特征来定义。

### 6.3 融合视觉信息与语义信息的方法

#### Multimodal FCN [18]

​	MFCNN以端到端的方式，逐像素同时辨别其基于视觉和语义的类别。它是一个泛化的页面分割模型，可以基于语义功能对文字区域指定特定的标签以进行细粒度的识别。

​	为了在基于CNN的模型中融合文字信息，作者构建了一个文字嵌入图（Text Embedding Map），把它输送给了MFCNN。更具体地说，对每个句子计算其嵌入表示，将该嵌入映射给该语句所在区域的每一个像素点。

![1596342496828]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEJe5uH5m2Z*KonVNgdT3rR0M6ggR*9wZ0Hf0muFKILbjrUZjXC3e2OuYYSGaBaDwoBj6ODmzUjapkPj.qqQkUl8!/r )

​	为了解决训练数据的问题，作者提出了一个有效的合成文档生成方式，并用它生成了大规模的预训练数据。进一步地，作者提出了两个无监督任务用于更好的提升模型泛化性。其中，通过重建原始图像，重建任务有助于学到更好的表征；连续性任务鼓励同一区域的像素拥有相似的表征。

**ICDAR 2015数据集上的IoU分数表：**

| Methods             | non-text | text |
| ------------------- | -------- | ---- |
| Leptonica [23]      | 84.7     | 86.8 |
| Bukhari et al. [24] | 90.6     | 90.3 |
| Ours (binary)       | 94.5     | 91.0 |

| Methods               | figure | text |
| --------------------- | ------ | ---- |
| Fernandez et al. [20] | 70.1   | 85.8 |
| Ours (binary)         | 77.1   | 91.0 |

**SectLabel数据集上的F1分数表：**

| Methods           | section | caption | list  | para. |
| ----------------- | ------- | ------- | ----- | ----- |
| Luong et al. [21] | 0.916   | 0.781   | 0.712 | 0.969 |
| Ours              | 0.919   | 0.893   | 0.793 | 0.969 |

#### LayoutLM [1]

​		LayouLM是结合了文档视觉结构以及文本语义信息的通用文档预训练模型。它在Bert模型基础上添加了2-D Position Embedding 和Image Embedding两种新的Embedding层来有效地结合文档视觉和结构信息。

- 2-D Position Embedding生成方法：通过OCR获取每个文字行内的所有单词以其边界框坐标(x0, y0, x1, y1)，将文字行内所有单词的(xmin, ymin, xmax, ymax)分别做embedding，这4个embedding结果的和作为最终的2-D Position Embedding；
- Image Embedding生成方法：采用Faster RCNN对每个单词区域和整张文档图像提取特征；
- 将2-D Position Embedding通过预训练的Bert得到LayoutLM Embedding，对LayoutLM Embedding和Image Embedding求和得到最终特征，用于开展下游任务。

<img src="https://i.loli.net/2020/08/05/meYX1cswORyoH53.png" width="1000" />

​		在预训练阶段，LayoutLM采用了MVLM遮罩式视觉语言模型和MDC多标签文档分类两个任务，并以IIT-CDIP 数据集作为训练集进行完全预训练。

​		论文将预训练模型迁移到表单理解、票据理解两个下游任务中并且都取得了目前的最佳成绩。

**表单理解（Form Understanding）**

​		在表单理解任务上，使用 FUNSD 作为测试数据集，该数据集中的199个标注文档包含31,485个词和9,707个语义实体。在该数据集上，需要对数据集中的表单进行键值对（key-value）抽取。通过引入位置信息的预训练，LayoutLM 在该任务上取得了显著的提升。实验结果见下表：

<div align="center"><img src="https://i.loli.net/2020/08/05/nSFa2G5V8qAJTd1.png"  width="900" /></div>

**票据理解 （Receipt Understanding）**

​		在票据理解任务中，选择 SROIE 比赛数据集作为数据集，其包含1000张已标注的票据，每张票据标注了company，date，address，total四个语义实体。通过在该数据集上微调，LayoutLM的表现比 RDCL 2019(ICDAR Competition on Recognition of Documents with Complex Layouts) 比赛第一名F1 值高1.2个百分点，达到95.24%。其实验结果如下：

<div align="center"><img src="https://i.loli.net/2020/08/05/QP6Zlcf1HpgYIXh.png"  width="900" /></div>

## 7. 基于目标检测的语义分割

- DeepDeSRT: Deep Learning for Detection and Structure Recognition of Tables in Document Images. ICDAR, 2017
- Fast CNN-based document layout analysis. ICCV, 2017
- DeCNT: Deep deformable CNN for table detection. IEEE Access, 2018.
- Graphical object detection using Mask R-CNN ICDAR, 2019.
- Table detection using YOLO. ICDAR, 2019.

![1596419804068]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEFuIMA1KftuWbGVyiqGD1NgKgRj5zXHYB1nnuwxYpisFFFPyL.K5C8v.MP2T.GsMxup7Zq7yOh58BkTrqQW*FF4!/r )

#### Visual Detection with Context for Document Layout Analysis [17]

​		这篇文章中，作者提出了将上下文信息加入到特征当中用于Faster RCNN对bounding box的分类和回归；除此之外，作者标注了一个新的论文数据集，其中包括9个类别，100篇文章的822个页面。实验结果表明，结合了上下文信息的特征使模型在作者制作的数据集上的mAP提升了23.9%。并且，该方法比基于文本的方法快14倍。

<div align="center"><img src="http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqbsZaGi7GGusZkdsW6ISQWCwxb1*ErwkLbgUStPdp2NgxQpiRtNPeLwEwkVnuAtCMEOCx9iutEl6qPyerMMqESQ!/b&bo=uwERAbsBEQEDCSw!&rf=viewer_4" /></div>

​		Baseline的mAP为46.38%，表现最好的类是“正文”，其AP为87.49%，表现最糟糕的类是“作者”，其AP为1.22%。作者融合到特征中的上下文信息如下：

- 页面上下文：当前页的页码和文档的总页面数，二者均被标准化到数据集中文档的平均页数：8.22。

- 边界框上下文：RoI的位置和大小，均被标准化到图像的维度。

  二者被加入到了用于批RoIs的池化后特征中，而后用于分类和回归。

  融合了上下文特征的模型分数如下：mAP为70.3%，表现最好的类是”正文“，其AP为93.58%，表现最糟糕的类是"作者"，其AP为10.34%。

<div align="center"><img src="http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEJkWGGOfEsT0z01H2Px.KG4thtKvcP8bYlmrjY2X3zNC0m*DFUoD8oPpc1iOGh.YtCyPgBClJoR92rLNkUgY*Ig!/b&bo=iAOsAYgDrAEDGTw!&rf=viewer_4" /></div>

## 8. 参考文献

[1] Yiheng Xu, Minghao Li, Lei Cui, Shaohan Huang, Furu Wei and Ming Zhou - **LayoutLM: Pre-training of Text and Layout for Document Image Understanding** -  *ACM SIGKDD Conference on Knowledge Discovery and Data Mining*

[2] https://guillaumejaume.github.io/FUNSD/

[3] G¨obel, M., Hassan, T., Oro, E. and Orsi, G. - **ICDAR 2013 table competition.** - *12th International Conference on Document Analysis and Recognition*

[4] Gao, L., Yi, X., Jiang, Z., Hao, L. and Tang, Z. - **ICDAR 2017 competition on page object detection.** -*14th International Conference on Document Analysis and Recognition*

[5] https://rrc.cvc.uab.es/?ch=13&com=downloads

[6] https://www.primaresearch.org/RDCL2019/ 

[7] Gao, L., Djean, H., Yan, Q., Kleber, F., Huang, Y., Meunier, J.L. and Fang, Y. - **ICDAR 2019 competition on table detection and recognition (cTDaR).** - *15th International Conference on Document Analysis and Recognition*

[8] http://personal.psu.edu/xuy111/projects/cvpr2017_doc.html

[9] Fang, J., Tao, X., Tang, Z., Qiu, R. and Liu, Y. - **Dataset, ground-truth and performance metrics for table detection evaluation.** - *IAPR International Workshop on Document Analysis System 2012*

[10] Shahab, A., Shafait, F., Kieninger, T. and Dengel, A. - **An open approach towards the benchmarking of table structure recognition systems.** - *Document Analysis System 2010*

[11] Ajoy Mondal, Peter Lipps and [C. V. Jawahar](http://cvit.iiit.ac.in/people/cvit-faculty?view=article&id=8:jawahar&catid=10:faculty) -  **IIIT-AR-13K: A New Dataset for Graphical Object Detection in Documents** - *14th IAPR International Workshop on Document Analysis System* 

[12] Xu Zhong, Jianbin Tang and Antonio Jimeno Yepes - **PubLayNet: largest dataset ever for document layout analysis** - *15th International Conference on Document Analysis and Recognition*

[13] Minghao Li, Lei Cui, Shaohan Huang, Furu Wei, Ming Zhou and Zhoujun Li - **TableBank: A Benchmark Dataset for Table Detection and Recognition** - *15th International Conference on Document Analysis and Recognition*

[14] Minghao Li, Yiheng Xu, Lei Cui, Shaohan Huang, Furu Wei, Zhoujun Li and Ming Zhou - **DocBank: A Benchmark Dataset for Document Layout Analysis** - ***[ arXiv:2006.01038](https://arxiv.org/abs/2006.01038)***

[15] Dafang He, Scott Cohen, Brian Price, Daniel Kifer and C. Lee Giles - **Multi-Scale Multi-Task FCN for Semantic Page Segmentation and Table Detection** - *14th International Conference on Document Analysis and Recognition*

[16] Rasmus Berg Palm, Ole Winther and Florian Laws - **CloudScan - A Configuration-Free Invoice Analysis System Using Recurrent Neural Networks** - *14th International Conference on Document Analysis and Recognition*

[17] Carlos Soto and Shinjae Yoo - **Visual Detection with Context for Document Layout Analysis** - *Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing and the 9th International Joint Conference on Natural Language Processing (EMNLP-IJCNLP)*

[18] Xiao Yang, Ersin Yumer, Paul Asente, Mike Kraley, Daniel Kifer and C. Lee Giles - **Learning to Extract Semantic Structure From Documents Using Multimodal Fully Convolutional Neural Networks** -  *Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2017, pp. 5315-5324*

[19] Anoop Raveendra Katti, Christian Reisswig, Cordula Guder, Sebastian Brarda, Steffen Bickel, Johannes Höhne and Jean Baptiste Faddoul - **Chargrid: Towards Understanding 2D Documents** - *EMNLP 2018*

[20] Timo I. Denk and Christian Reisswig - **BERTgrid: Contextualized Embedding for 2D Document Representation and Understanding** - *"Document Intelligence" workshop of 33rd Conference on Neural Information Processing Systems (NeurIPS 2019)*

[21] Xiaohui Zhao, Endi Niu, Zhuo Wu and Xiaoguang Wang - **CUTIE: Learning to Understand Documents with Convolutional Universal Text Information Extractor** - *CVPR 2019*

[22] Xiaojing Liu, Feiyu Gao, Qiong Zhang and Huasha Zhao - **Graph Convolution for Multimodal Information Extraction from Visually Rich Documents** - *NAACL 2019*

[23] D. S. Bloomberg and L. Vincent. - **Document image applications.** - *Morphologie Mathmatique, 2007. 8*

[24] S. S. Bukhari, F. Shafait, and T. M. Breuel. - **Improved document image segmentation algorithm using multi resolution morphology.** - *In IS&T/SPIE Electronic Imaging, pages 78740D–78740D. International Society for Optics and Photonics, 2011. 8* 

[25] F. C. Fernandez and O. R. Terrades. - **Document segmentation using relative location features.** - *In Pattern Recognition (ICPR), 2012 21st International Conference on, pages 1562–1565. IEEE, 2012. 8*

[26] M.-T. Luong, T. D. Nguyen, and M.-Y. Kan. - **Logical structure recovery in scholarly articles with rich document features.** - *Multimedia Storage and Retrieval Innovations for Digital Library Systems, 270, 2012. 2, 6, 8* 

