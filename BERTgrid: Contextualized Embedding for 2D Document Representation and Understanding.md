## BERTgrid: Contextualized Embedding for 2D Document Representation and Understanding

### Model

[C+BERTgrid] : combines the Chargrid and BERTgrid input representations.  

[Wordgrid] : Identical to Chargrid in that it is non-contextualized, learned with word2vec.

### Experiments

[Wordgrid] consistently performs worse on all fields, which can be attributed to the high rate of out-of-vocabulary words. Only when combining word-and character-level information in [C+Wordgrid], we outperform the baseline on most fields. Our contributions [BERTgrid] and [C+BERTgrid] significantly outperform all other models.  

We assume the performance of BERTgrid stems from (i) embedding on the word-piece level and (ii) contextualization. We observe that both [C+Wordgrid] and [C+BERTgrid] converge faster than [Chargrid].  

