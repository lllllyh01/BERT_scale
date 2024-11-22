# Week3
## BERT vs. GPT
#### Differences
**BERT:**
1. bi-directional, able to understand the context from previous and later words
2. Trained by predicting masked words and next sentences
3. Based on multiple encoders
   
<br>

**GPT:** 
1. Unidirectional, only linking with previous contexts
2. Trained by predicting the next sentences. No masks, just generate text autoregressively

#### Scales
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

#### Questions
1. Because of the training method, will GPT and BERT have advantages in different tasks? E.g, GPT is good at generation-based tasks, BERT is good at understanding-based tasks, etc. How to justify the comparison?
  
    Solutions:

     - First step: proof that scale up BERT will boost its performance, and it can be competitive with GPT
     - Compare with head-to-head tasks: summarize, etc.
1. The size of training data also matters
    
    Solutions:
    
     - Keep finetuning dataset identical
     - Look up the original paper and figure out the specific training dataset size

#### TODO
1. Develop small GPT and BERT
2. Read Flash attention paper https://arxiv.org/abs/2307.08691


# Week4
### Done
1. Developed the training and testing scripts for BERT and GPT
2. Experiments for small scale BERT and GPT ongoing
3. (Problem from last week) pretraining dataset & size
   1. GPT1: BooksCorpus dataset (7,000 unpublished books, 6G)
   2. BERT: BooksCorpus (800M words) and English Wikipedia (2,500M words, 16G).
   ---
   3. GPT2: WebText, 8 million documents (40G)
   4. RoBERTa-base: BooksCorpus, Wikipedia (16G)
      - additional data: CC-NEWS, OPENWEBTEXT, STORIES (160G in total)
   5. DeBERTa: BookCorpus, Wikipedia, OPENWEBTEXT, STORIES (78G)

### TODO
1. Waiting for the small model results


# Week 5-6
### Done
**Model Settings:** <br>
Downstream task: text summarization <br>
Dataset: CNN Daily Mail 3.0.0, 287,113 train data, 13,368 validation data, 11,490 test data. <br>
Fintuning data size: 10,000, Test data size: 500, <br>
Max length=512, <br>
epochs=3, <br>
train_batch_size=4, <br>
Optimizer=AdamW, warmup_steps=500, weight_decay=0.01 <br>

**Results:** <br>
1. Small GPT: ROUGE-1: 0.3338, ROUGE-2: 0.1381, ROUGE-L: 0.2251
2. Small BERT: ROUGE-1: 0.0312, ROUGE-2: 0.0000, ROUGE-L: 0.0260
   
   **Generated Summary 1**: 

   **Reference Summary 1**: Membership gives the ICC jurisdiction over alleged crimes committed in Palestinian territories since last June .
   Israel and the United States opposed the move, which could open the door to war crimes investigations against Israelis .

   **Generated Summary 2**: 

   **Reference Summary 2**: Theia, a bully breed mix, was apparently hit by a car, whacked with a hammer and buried in a field .
   "She's a true miracle dog and she deserves a good life," says Sara Mellado, who is looking for a home for Theia .

   **Generated Summary 3**: iran's prime minister mir hossein moussavi says he's disappointed in iran's failure to secure stability. he says iran has failed to secure stability in its own hands. he says iran has failed to secure stability in its own hands.

   **Reference Summary 3**: Mohammad Javad Zarif has spent more time with John Kerry than any other foreign minister .
   He once participated in a takeover of the Iranian Consulate in San Francisco .
   The Iranian foreign minister tweets in English .

### Problems & TODO
1. Since BERT is not a generative model, it need encoder and decoder to generate text summarization, making the total parameters twice of the same size of GPT. Should we keep the size of base model, or complete model the same, to make them comparable?
2. Training hyperparameters finetuning
3. Training is super slow if finetuning entire model. Using PEFT (LoRA) instead.

# Week 7-8
### Done
1. Experiment results on small scale BERT and GPT (about 130 million parameters):

   Dataset: CNN Daily Mail dataset for text summarization. Used 60,000 training data, 1,000 testing data.
   **GPT rougeL: 0.132, BERT rougeL: 0.21**

   Both GPT and BERT were pretrained on large language dataset. Here BERT model is actually BART (a BERT encoder + GPT decoder). 
   
   I also tried pure BERT structure (BERT encoder + BERT decoder), but the results were not that good. It may because that as an encoder-only structure, BERT didn't pretrained on generation tasks, which made it perform poor on text summarization.