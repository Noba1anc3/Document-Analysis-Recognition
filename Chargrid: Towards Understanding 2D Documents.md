## Document Understanding with Chargrid

### Chargrid

The complete text of a document page can thus be represented as a set of tuples D = {(ck,bk)|k=0,1,2,...,n}, where ck denotes the k-th character in the page and bk the associated character box of the k-th character, which is formalized by the top-left pixel position, width and height, thus bk = (xk, yk, wk, hk).



The advantage of the new chargrid representation:

- encode a character by a single scalar value
- downsample the chargrid representation without loss of any information, reduce the time complexity



A character can occupy a region spanning several character pixels. The larger a given character, the more character-pixels represent that single character. It helps since it implicitly encodes additional information, for example, the font size.



Before the chargrid sent to neural network, apply 1-hot encoding to the chargrid g.  
$$
g \in N^{H×W} => \widetilde g \in N^{H×W×N}
$$
N denotes the number of characters in the vocabulary including background and unknown character.

### Network Architecture

As there can be multiple and an unknown number of instances of the same class, we further perform instance segmentation. This means, in addition to predicting a segmentation mask, we may also predict bounding boxes using the techniques from object detection.



Encoder : VGG + dilated conv + batch norm + spatial dropout  

Stride-2 convolutions to yield slightly better results compared to max pooling.

Whenever we downsample, we increase the number of channels by a factor of two.  



Decoder are both made of conv blocks which essentially reverse the downsampling of the encoder via stride-2 transposed conv.  

Each block first concatenates features from the encoder via lateral connections followed by 1 x 1 conv.  

Whenever we upsample, we decrease the number of channels by a factor of two.



Decoder for semseg has an additional conv layer without bn but with bias and softmax.  

Decoder for bbox regression task forms a one-stage detector which makes use of focal loss.



The number of output channels are 2N for box mask(foreground versus background) and 4N for four box coordinates, where N is the number of anchors per pixel.  

## IE from Invoices

### Evaluation Measure

For a given field, we count the number of insertions, deletions, and modifications of the predicted instances to match the ground truth instances. N is the total number of instances occurring in the gt of the entire test set.  
$$
1- \frac {\#[insertions]+\#[deletions]+\#[modification]} N
$$
