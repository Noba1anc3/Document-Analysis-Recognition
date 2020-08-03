## 文档理解

![1596418728900](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqbW5R1*DATbMs2rMyXVhKuTYJ1JURggHEtf6cGF*vGNAIm2jWo1w791V.CSI3NkdTww4mCrRcrVRVwe803cvDfQ!/b&bo=uwPxAbsD8QEDCSw!&rf=viewer_4)

![1596418889611](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrED5Ll.FC4PiT3wCDfGukTwzxU37V8MkItnRj4IkEVlZH1c*r0cTANomT94h5SCzH1gWlmbbixKMdlAfUPpumXDk!/r)

![1596418903848]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEJdUqzrMaWKZFba.wsx4R9*vWtJEFTS0QCZurf8Hz7Wj13ywuBezLB2vIFs59P2irvF4FTeIpR.dIX.n*S77vcI!/r )



## 1.文档语义分割

### 语义分割的定义

​		语义分割是当今计算机视觉领域的关键问题之一。从宏观上看，语义分割是一项高层次任务，为实现场景的完整理解铺平了道路。场景理解作为一个核心计算机视觉问题，其重要性在于越来越多的应用程序通过从图像中推断知识来提供营养。其中一些应用包括自动驾驶，人机交互，虚拟现实等。 其涉及将一些原始数据（例如，平面图像）作为输入并将它们转换为具有突出显示的感兴趣区域的掩模。许多人使用术语全像素语义分割（full-pixel semantic segmentation），其中图像中的每个像素根据其所属的感兴趣对象被分配类别。 

### 文档语义分割的定义

​		文档语义分割在学术上尚且没有一个统一的定义，但总体而言都是在解决同一个问题，即在文档图像上的语义分割任务。进一步地，文档语义分割可以分类为OCR前的语义分割和OCR后的语义分割，在此选取两篇论文中的定义来阐述。

![1596420457262]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEK0sKe8cnyDZUZBs1KWk64OBd5iMFqfGlMS41sRCqxvSi2ZXXarVpNbiuOebb0RXlfjpeOghrKPQQ6J4SMSI7AI!/r )

![1596420468285](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrENGrtySjFhQ8TF5UgHj8hIqSzj8RsLRO*cCOzpvtTDRvk8Eri*I3B5siBs6QSGOpq.kkLpTmbHdi8IQQ55ir0ig!/b&bo=SQOMAEkDjAADGTw!&rf=viewer_4)

#### OCR前语义分割

​		对于OCR前的语义分割，Bukhari 等人在 DAS 2010 中发表的论文的表述如下 : “文档图像的语义分割将文档分割为文字和非文字区域，是文档图像分析任务中提升OCR结果的一个十分重要的预处理步骤”。也就是说，OCR前的语义分割通常将文档图像分割为文字，图片和表格区域。对于分割出的文字部分，可利用相关算法进行文字检测和识别。对于分割出的图片部分，可使用图像分析算法进行解析。对于分割出的表格部分，可使用表格理解算法进行表格理解。

![1596427227229](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEJ61FQaImMR6n1MlTCfM8QfXVf1u99bSqcpyI9s4FOf.ByrK7EpFQoYEL0rloyUqCMwqbK3QuQJXacDyo6k8FbQ!/r )

#### OCR后语义分割

​		对于OCR后的语义分割，通常又被称作文档信息抽取，文档版面分析和文档语义结构提取。Yang 等人在 CVPR 2017 中发表的论文的表述如下 : "我们将文档语义结构提取看作一个逐像素的语义分割任务，并提出了一个统一的模型，该模型不同于传统的版面分割任务，仅仅基于视觉来分类像素"。换言之，OCR后的语义分割任务更多的融合了文字的语义信息和上下文信息，可以更好的找到更详尽的语义类型，用于文档的版面分析于信息抽取当中。

![1596436426620](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEF58Y*o9EtyL*X6ehd7xV8ntlXxUBywxjc3tLfXLIyDus3tvtZ14T4dOR5kEIJRDPoEX7*49YXjINCev1phYvRE!/r )

![1596436467871](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEFMtLyATAFC70E*kNS9sWWLulUrFfd03bDi6qjuvg81lLwxkt4mqJ*ncEb2eMZasJRKydfhe*091iPLZrwwxAm0!/r )

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

### CloudScan - 基于循环神经网络的免配置发票分析系统

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

## 3.基于逐像素分类的语义分割

- Multi-scale Multi-task FCN for Semantic Page Segmentation and Table Detection. ICDAR, 2017.
- Learning  to Extract Semantic Structure from Documents Using Multimodal Fully Convolutional Neural Networks. CVPR, 2017.
- Fully Convolutional Neural Networks for Page Segmentation of Historical Document Images. DAS, 2018.
- Multi-task layout analysis for historical handwritten documents using Fully Convolutional Networks. IJCAL, 2018.
- Graphical object detection in document images. ICDAR, 2019.
- Semantic Structure Extraction on Deformed Documents via Fully Convolutional Networks.
- LayoutLM: Pre-training of Text and Layout for Document Image Understanding. KDD, 2020

![1596419779084](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEGkTzgIs42v92hurpJuXmPoT7iZU.2ZyD59bsyY1ZeTncziquQQrtu6CqZ.sOWtAjFloZ2nW8s1mL28EzB8o0oc!/r)

逐像素分类的语义分割方法通常

### 基于视觉信息的方法

#### Multi-scale Multi-task FCN

​		在MMFCN当中，作者第一次用一个统一的深度学习框架同时解决语义分割和表格检测的任务，亦是第一次使用深度神经网络来生成实例的边界。此外，作者提出了一个新的合成文档方法，用合成文档训练出的模型在真实文档上取得了不错的结果。

​		其合成文档的生成效果如下：

![1596437866975](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEKDjPSucZE8JONI2rMOydVxepZ6wEPN8GcufoCgAs6f.95jOVhRb1UNc5ppBDbWeeuIS9BrMysQQuIYFkcq.qhM!/r)

​		MMFCN的网络框架分为语义分割和轮廓检测网络。语义分割网络逐像素预测其概率，轮廓检测网络则预测元素实例的边界。而后，将语义分割和轮廓检测网络输出的特征输入到条件随机场当中，以精确语义分割网络的输出。除此之外，作者基于语义分割的结果，利用了一些启发式规则来提取每个表格实例，并利用一个验证网络来降低假阳率。

![1596437921072](http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEBMLNilHfB7z*oMFno0HkCRD1rze3J*nkOkUbf2gUnVj6qHgMSCmxXgBzDqIRFxF8Vzfen6n7hGk78.LBluMogI!/r)

​		作者提出的MMFCN是一个统一的框架，结合了深度学习模型和启发式规则来同时处理语义分割和表格检测两个任务。其中，预测类别和轮廓检测两个任务作为神经网络框架的两个分支同时训练。而对于后面的条件随机场，其一元项由语义分割网络输出的特征来定义，其成对项由色差和轮廓特征来定义。

### 融合视觉信息与语义信息的方法

#### Multimodal FCN

​	MFCNN以端到端的方式，逐像素同时辨别其基于视觉和语义的类别。它是一个泛化的页面分割模型，可以基于语义功能对文字区域指定特定的标签以进行细粒度的识别。

​	为了在基于CNN的模型中融合文字信息，作者构建了一个文字嵌入图（Text Embedding Map），把它输送给了MFCNN。更具体地说，对每个句子计算其嵌入表示，将该嵌入映射给该语句所在区域的每一个像素点。

![1596342496828]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEJe5uH5m2Z*KonVNgdT3rR0M6ggR*9wZ0Hf0muFKILbjrUZjXC3e2OuYYSGaBaDwoBj6ODmzUjapkPj.qqQkUl8!/r )

​	为了解决训练数据的问题，作者提出了一个有效的合成文档生成方式，并用它生成了大规模的预训练数据。进一步地，作者提出了两个无监督任务用于更好的提升模型泛化性。其中，通过重建原始图像，重建任务有助于学到更好的表征；连续性任务鼓励同一区域的像素拥有相似的表征。

#### LayoutLM



## 4.基于目标检测的语义分割

- DeepDeSRT: Deep Learning for Detection and Structure Recognition of Tables in Document Images. ICDAR, 2017
- Fast CNN-based document layout analysis. ICCV, 2017
- DeCNT: Deep deformable CNN for table detection. IEEE Access, 2018.
- Graphical object detection using Mask R-CNN ICDAR, 2019.
- Table detection using YOLO. ICDAR, 2019.

![1596419804068]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEFuIMA1KftuWbGVyiqGD1NgKgRj5zXHYB1nnuwxYpisFFFPyL.K5C8v.MP2T.GsMxup7Zq7yOh58BkTrqQW*FF4!/r )

## 5.数据集

​		语义分割模型的训练需要庞大的训练数据，从2010年开始陆续出现了若干具有一定规模的语义分割数据集。这些数据集有些专注于表格检测的任务，有些致力于版面分割的任务，近一两年来出现了拥有更多细粒度标签的大规模语义分割数据集，诸如PubLayNet和DocBank。随着时间的推移，数据集的制作方式由人工标注转变为基于规则的弱监督生成，数据集的大小与日俱增，训练出来的语义分割模型也随之越来越强大。这使得基于大规模多领域数据集的语义分割预训练模型的设想成为现实[14]。

![1596436245954]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEOzIanVWLWA8mkhyQMEPUgvn5gKq.t7tPStAGLeHhO*UfgY1iL0uGr9yJMtCFvQr48xpDRPFq2HVwnk..0HK5hw!/r )

![1596436155245]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrELLAEF2TedUovX52*rJV3X**4ySrGDKO8llKmhOZjzshvhDUgJB6Y9YoCaYfhtg8E6heJiQjzi0Qebm30KoABHU!/r )

### ICDAR 2013 [16]

​		该数据集是表格检测和结构识别任务中引用最多的数据集之一。它包含67个PDF，对应238页图像。其中40份来自美国政府，27份来自欧盟。在238页图像中，只有135页图像包含表，共有150个表。该数据集被广泛用于表检测和结构识别任务的算法评估。

###  ICDAR-POD-2017 [17]

​		它着重于检测文档图像中的各种图形对象（如表格、公式和图形），通过从CiteSeer的1500篇科学论文中选出的2417个文档图像来创建。它包括多种多样的页面布局—单列、双列、多列，以及对象结构的显著变化。该数据集被分成（i）由1600个图像组成的训练集，和（ii）包含817个图像的测试集。

### ICDAR RDCL [21]

ICDAR RDCL是文档分析与识别国际会议复杂版面文档识别竞赛的简称，每两年举办一次。比赛使用的数据集为PRImA版面分析数据集，由曼彻斯特萨福德大学PRImA实验室提出，包括当代杂志和科学文章之内的扫面页。其主要任务是进行版面分割和区域分类。

![1596451116804]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEPPOa0rFR7ADEpP546LN1rIcatM2Upr7*6JeI7GhN2aSi6nUa62sHWCQrVGfv8LfJyCJ4PbpZS.zYTcp1wKmrHQ!/r )

### cTDAR [18]

​		该数据集由各种格式的现代文献和存档文档组成，包括文档图像和PDF等数字格式。这些图像显示了各种各样的表格，从手工绘制的会计账簿到证券交易清单、火车时刻表、囚犯名单记录簿、印刷书籍表格、生产普查等。现代文献包括科学期刊、表格、财务报表等。注释与表区域相对应，单元格区域可用。该数据集包含（i）训练集-由600个带标注的档案和600个带表格边界框的现代注释文档图像组成，以及（ii）测试集-包括199个带注释的档案和240个带表格边框的现代文档图像。

### Marmot [19]

​		Marmot 数据集由北京大学王选计算机研究所网络内容保护与文档处理研究室制作，它由2000页中英文组成，比例约为1 : 1。中文网页选自方正阿帕比图书馆提供的120多种不同主题的电子书，其中在每本书中选取不超过15页。英文版选自Citeseer网站1970-2011年间出版的1500多篇期刊和会议论文。页面显示了各种各样的布局—一列和两列、语言类型和表格样式。此数据集用于表格检测和结构识别任务。

### UNLV [20]

​		它包含2889个文档图像，包括技术报告、杂志、商业信函、报纸等，其中只有427个图像包含558个表格。表区域和单元格区域的注释可用。此数据集还用于表格检测和表结构识别任务。

### PubLayNet [13]

​		PubLayNet是一个大型文档图像数据集，文档布局同时使用边界框和多边形进行标注。其使用的原始文档是PubMed中心开源数据集，通过自动化对齐PDF解析结果和XML文件来完成对文档的标注。该工作获得了2019年ICDAR的最佳论文奖。

![1596450718853]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEF.NhDQK9IhR9XnLv6mfQJntby9xaSmnJQiGyl.Ul6neCXZEqLsjDOUUnjCf3rUh.Yt.svCCpra5GulVf8iaafY!/r )

### TableBank [11]

​		TableBank是由北航与微软亚洲研究院联合提出的表格检测与识别新型数据集。该数据集是通过对网上的Word和Latex文档进行弱监督而建立的，不同于传统的弱监督数据集，作者使用的方法可以获得大规模且高质量的训练数据。其包含417,234个高质量标注表格，并且这些表格所在的文档有着各式各样的领域。

| Task                        | Word    | Latex   | Word+Latex |
| --------------------------- | ------- | ------- | ---------- |
| Table detection             | 163,417 | 253,817 | 417,234    |
| Table structure recognition | 56,866  | 88,597  | 145,463    |

![1596442961694]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEK7YgC7eevq2N3h8WSTG*reaxWRlyh4jGB91NXc1lhrq2TkZgNBZtL.6SLqRr3vUxOYGPvV02.vrny5nN6uz6BI!/r )

### DocBank [12]

​		DocBank是由北航，哈工大和微软亚洲研究院联合提出的文档版面分析数据集。与TableBank一样，同样使用弱监督的方法来建立，拥有细粒度的token级标注。该数据集使在下游任务训练的模型可以同时学习到文本的和版面的信息。目前的DocBank包含500K个文档页码，其中400K张用于训练，50K张用于验证，50K张用于测试。

![1596444872518]( http://r.photo.store.qq.com/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEHJHm7msFudCMv2M8seHuyEONHlfeE4xZodg382PTNnuEJKg7iPYHE2kVQ34rfW4xlCDDI.Cm0EY9I.nrr.2Nuk!/r )

​		在文档版面分析任务中，已有一些基于图像的文档版面数据集，而这些数据集大多是针对计算机视觉方法构建的，很难应用于NLP方法。另外，基于图像的数据集主要包括页面图像和大型语义结构的边界框，它们不是细粒度的token级标注。此外，生成人工标记的细粒度token级文本块排列也是耗时和费力的。因此，利用弱监督以最小的努力获得细粒度的标记文档，同时使数据能够易于应用到任意的NLP和计算机视觉方法是至关重要的。

| Dataset         | #Pages  | #Units | Image-based? | Text-based? | Fine-grained? | Extendable? |
| --------------- | ------- | ------ | ------------ | ----------- | ------------- | ----------- |
| Article Regions | 100     | 9      | ✔            | ✘           | ✔             | ✘           |
| GROTOAP2        | 119,334 | 22     | ✔            | ✘           | ✘             | ✘           |
| PubLayNet       | 364,232 | 5      | ✔            | ✘           | ✔             | ✘           |
| TableBank       | 417,234 | 1      | ✔            | ✘           | ✔             | ✔           |
| DocBank         | 500,000 | 12     | ✔            | ✔           | ✔             | ✔           |

### IIIT-AR-13K [DAS 2020]

​		IIIT-AR-13K由印度国际信息技术学院提出，该数据集通过手工标注公开企业年报制作，一共包含13K张图片。数据集内的元素有以下五个类别：表格，图片，自然图片，LOGO和签名。这是目前最大的图像目标检测手工标注数据集。数据来源于不同语言的多家公司在若干年来发布的企业年报，这给数据集带来了很大的多样性。

## 6.评价指标

### Precision - Recall - F1

### mAP

### IoU

## 7.参考文献

[10] https://www.icst.pku.edu.cn/cpdp/sjzy/index.htm 

[11] Minghao Li, Lei Cui, Shaohan Huang, Furu Wei, Ming Zhou and Zhoujun Li - **TableBank: A Benchmark Dataset for Table Detection and Recognition** - *15th International Conference on Document Analysis and Recognition*

[12] Minghao Li, Yiheng Xu, Lei Cui, Shaohan Huang, Furu Wei, Zhoujun Li and Ming Zhou - **DocBank: A Benchmark Dataset for Document Layout Analysis** - ***[ arXiv:2006.01038](https://arxiv.org/abs/2006.01038)***

[13] Xu Zhong, Jianbin Tang and Antonio Jimeno Yepes - **PubLayNet: largest dataset ever for document layout analysis** - *15th International Conference on Document Analysis and Recognition*

[14] Yiheng Xu, Minghao Li, Lei Cui, Shaohan Huang, Furu Wei and Ming Zhou - **LayoutLM: Pre-training of Text and Layout for Document Image Understanding** -  *ACM SIGKDD Conference on Knowledge Discovery and Data Mining*

[15] Ajoy Mondal, Peter Lipps and [C. V. Jawahar](http://cvit.iiit.ac.in/people/cvit-faculty?view=article&id=8:jawahar&catid=10:faculty) -  **IIIT-AR-13K: A New Dataset for Graphical Object Detection in Documents** - *14th IAPR International Workshop on Document Analysis System* 

[16]  G¨obel, M., Hassan, T., Oro, E. and Orsi, G. - **ICDAR 2013 table competition.** - *12th International Conference on Document Analysis and Recognition*

[17]  Gao, L., Yi, X., Jiang, Z., Hao, L. and Tang, Z. - **ICDAR 2017 competition on page object detection.** -*14th International Conference on Document Analysis and Recognition*

[18]  Gao, L., Djean, H., Yan, Q., Kleber, F., Huang, Y., Meunier, J.L. and Fang, Y. - **ICDAR 2019 competition on table detection and recognition (cTDaR).** - *15th International Conference on Document Analysis and Recognition*

[19]  Fang, J., Tao, X., Tang, Z., Qiu, R. and Liu, Y. - **Dataset, ground-truth and performance metrics for table detection evaluation.** - *WDAS (2012)*

[20] Shahab, A., Shafait, F., Kieninger, T. and Dengel, A. - **An open approach towards the benchmarking of table structure recognition systems.** - *Document Analysis System 2010*

[21]  https://www.primaresearch.org/RDCL2019/ 
