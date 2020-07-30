### Multi-scale Multi-task FCN for Semantic Page Segmentation and Table Detection

2017 ICDAR   Penn State Univ. + Adobe Research  

#### Introduction
论文用途：整合sota方法分割文字，表格和图片  
MMFCN分成两个网络，语义分割网络和轮廓检测网络。语义分割网络逐像素预测概率，轮廓检测网络预测元素实例的边界。  
将语义分割和轮廓检测网络输出的特征输入到条件随机场crf中，以精确语义分割网络的输出。  
基于语义分割的结果，利用一些启发式规则来提取每一个表格实例，并利用一个验证网络降低假阳率。  

作者提出的MMFCN是一个统一框架，结合了深度学习模型和启发式规则来同时处理语义分割和表格检测两个任务。  
预测类别和边界两个任务作为两个分支同时训练。  
CRF的一元项由语义分割网络输出的特征定义，成对项由色差和轮廓特征来定义

#### Contribution
作者的贡献：  
1. 用一个统一的深度网络框架同时解决语义分割和表格检测的任务还是第一次
2. 用深度神经网络生成实例边界还是第一次
3. 提出了一个新的合成文档方法
4. 用合成文档训练出的模型在真实文档上取得了不错的效果

#### 合成文档
合成文档生成方式：先标记2000多张文档，用其他元素（图片，表格）随机替换被标注文档当中的元素。自然图片从ImageNet和MSCOCO两个数据集当中收集。表格的收集方式有两种，其中一个是从真实文档pdf中通过生成候选表格区域的方法得到2000个表格，而后标记每一个表格是不是正确的。另一种方式从互联网上爬取大量不同种类的表格图片。除此之外，利用一个大的文字语料库生成了许多表格。

![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqU7SR08fgiEzHugh4I9jTs*5h.9BSJ9ThhqN5jYyCbd*2MYCsKSYvQYaNHPNWVb3B1LjuP4kk3B.jvTSo4u4GcY!/b&bo=KwXlASsF5QEDCSw!&rf=viewer_4)

#### 网络结构
![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqabIF0a.xtPXR8hLK6bs4RvwD0tppS4bkfN20sqsoiAlU2SsPTXpewrwVQFQs3DuZtSv5Edo2nbpTQ1u7nF56Tw!/b&bo=DgVxAg4FcQIDCSw!&rf=viewer_4)

#### 多尺度
![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqdOqskqAFUQPuJkjioIhhtphbCKfzRfLegBlM01fM3KZVQnUnKpZ8flGa*RU5N3deXcGWP4FPQ9lweuYnf3Lzwo!/b&bo=oALMAaACzAEDCSw!&rf=viewer_4)

用VGG19初始化，后面接着unpooling和全卷积以放大特征图的尺度，使网络得到多尺度信息。对于语义分割和轮廓检测两个任务，都有两个尺度的特征图，每个任务最后的输出会把两个尺度的特征拼起来并接入后面的卷积。全卷积之后分两支，一支用于语义分割，使用NLL Loss；另一支用于边缘检测，用MSE Loss.

#### 语义分割的优化
多尺度预测的训练难过单尺度。作者使用了一个逐尺度强监督，训练方法被用在了若干此前的工作当中，被声称可以为每个尺度生成更具有判别性的特征。  
Loss如下：  
![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqTlVwjOp96YQVEw5H3hcv.dHrnS0bLGxcwcK3kHN9IuKuIjx8XeAV22u6BELnPv6Evk0MhOk9AYD8Imu8R666gw!/b&bo=hQKqAYUCqgEDCSw!&rf=viewer_4)

#### 边缘检测的优化
边缘被定义为一个像素集合包围了每一个文档元素实例。边缘把元素从其他元素或是背景当中区分开来。  
仅仅是把像素标记为0和1并不十分有效，原因如下：
1. 由于数据质量的缘故，gt可能会有微小的偏移
2. 把边缘预测偏移几个像素是可以接受的

如上所述，GT的定义如下：
![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqaTClf1aQek.gpIXEn94X5kFKHCXKugeTUp0zSk4lAsd0a7L.AP19lq8*w*7Yt3RYk.OFcJM1054qxkcxPKrGKM!/b&bo=WwKAAFsCgAADCSw!&rf=viewer_4)

Loss如下：  
![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqS2mv6LY0nvu.Y2inIiHBUhFa1PePTnVBfa7DoDjhDygNrN20TLhcaqAV5HfCTi3*zoUmk4T3ZJwjOQ7ThyjyOA!/b&bo=3QIXAd0CFwEDCSw!&rf=viewer_4)

#### 联合训练
![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEDfY3AopA*gf8VpKraNSUwQCjc1nug9q2XVaAbUwkuoSaxnhBkMLJXwksYe9DQ6EZjasoUvwIkwST89oS4Oa80I!/b&bo=1QIhAdUCIQEDGTw!&rf=viewer_4)

#### 条件随机场
全卷积网络预测出来的结果尝尝面临着预测出来的像素都是互相独立的，因此输出并不平滑连贯。  
常见的方法是在网络之上加一层CRF，以特征作为一元项，以色差作为二元项。然而在图片中，色差是不够的（参考表格），因此额外使用轮廓作为二元项。  
![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqQZdq*Qdaup35qmbbnzOh46Oqli4J3OIpJWszQyVWtiNUj*sXE3RxnSvuZnl3Q14IVGep.mpjDQItOnqGM95f.w!/b&bo=3AMQAtwDEAIDCSw!&rf=viewer_4)

接下来最小化能量E即可  
![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqQi6LPBsTuUwORU*7ALsNtm1kaG3LTfWpF2pv2sqcykpDXULu0aT3qfvcjX2zxOhBuS9yOZ.TBfinN9rbiJkLqk!/b&bo=2QI0ANkCNAADCSw!&rf=viewer_4)

#### 边缘检测效果
![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEJcOMo8*K4LuLMJlx53zx5WNxKIAC6aI2EEbeKMFDI0zfVGIRl*Q.cO81JJg9R42muvJtOMzHzSEfTXBIIj5Jl4!/b&bo=XARdAVwEXQEDORw!&rf=viewer_4)

#### 语义分割效果
![](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqSKZ9DsaXhJm1BvGrs8WfY8QgDtd5j*ayii3CDYaFS72w8L2kw05ezxjDhoEr4HWIyxKdKBI5d1K9CXk4KXgjz0!/b&bo=bwOmAm8DpgIDCSw!&rf=viewer_4)

#### 表格检测
在CRF之后，设置表格的概率掩膜阈值为0.5，之后使用CCA以得到表格可能的位置。为了移除假阳表格，在CCA后加入了一个CNN来分类每个区域是不是一个表格。这个卷积网络被称为验证网络，以预训练VGG16作为初始化。
