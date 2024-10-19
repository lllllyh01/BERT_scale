# BERT vs. GPT
## Differences
**BERT:**
1. bi-directional, able to understand the context from previous and later words
2. Trained by predicting masked words and next sentences
3. Based on multiple encoders
   
<br>

**GPT:** 
1. Unidirectional, only linking with previous contexts
2. Trained by predicting the next sentences. No masks, just generate text autoregressively

## Scales
**GPT:**

**GPT-1 (2018): 117 million**

GPT-2 (2018): Small: 124 million, **Medium: 355 million**, Large: 774 million, **XL: 1.5 billion**

GPT-3 (2020): 175 billion

GPT-4 (2023): may be trillion

<br>

**BERT:**

**BERT-base: 110 million**, large: 330 million

DistilBERT: 66 million

RoBERTa-base (2019): 125 million, **large: 355 million**

**DeBERTa: 1.5 billion**

## Questions
1. Because of the training method, will GPT and BERT have advantages in different tasks? E.g, GPT is good at generation-based tasks, BERT is good at understanding-based tasks, etc. How to justify the comparison?
  
    Solutions:

     - First step: proof that scale up BERT will boost its performance, and it can be competitive with GPT
     - Compare with head-to-head tasks: summarize, etc.
1. The size of training data also matters
    
    Solutions:
    
     - Keep finetuning dataset identical
     - Look up the original paper and figure out the specific training dataset size

## TODO
1. Develop small GPT and BERT
2. Read Flash attention paper https://arxiv.org/abs/2307.08691
