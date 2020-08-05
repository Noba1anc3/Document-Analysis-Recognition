# Visual Detection with Context for Document Layout Analysis

This is a somehow water paper. zzz

## Helpful Idea

augment some hand-crafted feature in Faster RCNN feature may improve the result

## Abstract

1. object detection technique augmented with contextual features
2. novel dataset of region-labeled articles (9 class, 100 articles and 822 article pages)

Initial experimental results demonstrate a 23.9% absolute improvement in mAP over the baseline model

Processing speed 14x faster than a text-based technique

## Related Work

Systems like CERMINE and OCR++ extract the raw or processed markup from 'born-digital' PDFs, apply semantic labels to text blocks.

Disadvantage

- rely on extracted PDF source markup
- work only on text blocks
- typically quite slow

Eskenazi et al. survey dozens of such methods.

## Visual Document Layout Detection

![1596572646165](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/bqQfVz5yrrGYSXMvKr.cqbsZaGi7GGusZkdsW6ISQWCwxb1*ErwkLbgUStPdp2NgxQpiRtNPeLwEwkVnuAtCMEOCx9iutEl6qPyerMMqESQ!/b&bo=uwERAbsBEQEDCSw!&rf=viewer_4)

Our approach incorporates contextual information about pages and ROI bounding boxes, encoded as additional features for the classification and fine-tuning regression stages of the model.  

The position, size, and page number of a candidate ROI in a document are valuable contextual clues to the true label of that region.  

Ease of integration and anticipated high impact on detection performance.

## Novel Labeled Dataset

New dataset is in PASCAL VOC format, sampled from the PMC Open Access set it has nine labeled region classes : title, authors, abstract, body, figure, figure caption, table, table caption, reference.

## Implementation and Experiments

![1596592477753](http://m.qpic.cn/psc?/V50VqFfH2A6OlZ2gWBDL0uxzNK4WmFgm/TmEUgtj9EK6.7V8ajmQrEJkWGGOfEsT0z01H2Px.KG4thtKvcP8bYlmrjY2X3zNC0m*DFUoD8oPpc1iOGh.YtCyPgBClJoR92rLNkUgY*Ig!/b&bo=iAOsAYgDrAEDGTw!&rf=viewer_4)

Baseline : Faster-RCNN-ResNet-101 Pretrained on ImageNet  

mAP : 46.38%  peak class performance on 'body' : 87.49%  lowest performance on 'author' : 1.22%  

Page context : page number of the current image in its article and the number of pages in the article, both normalized to the average page length of articles in the dataset (8.22)  

BBox context : position and size of the proposed region of interest, normalized to the dimensions of the image.  

Both were appended to the pooled feature vectors for batched ROIs sent to the classification and bbox regression.  

mAP : 70.3% peak class-performance on 'body' : 93.58% lowest performance on 'author' : 10.34%

## Discussion and Ongoing Work

New contextual features:

- ROI oversampling
- random feature map sampling
- all-region positional information
