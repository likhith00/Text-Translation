﻿# Text-Translation
This repository contains is implementation of text Translation use case.

# README

## Finetuning Helsinki-NLP/opus-mt-en-ro for english to romanian Translation

This repository contains code for finetuning the Helsinki-NLP/opus-mt-en-ro model on a text translation task with a dataset comprising english text and corresponding romanian translations.

### Task
- **Text Translation**: The task involves Translating English texts to Romanian.

### Model
- **Helsinki-NLP/opus-mt-en-ro**: machine translation model pretrained on parallel text data in English and Romanian

### Dataset
- **Dataset**: The dataset used is [likhith231/wmt_en_ro_7000](https://huggingface.co/datasets/likhith231/wmt_en_ro_7000). It is a truncated version of WMT dataset en-ro part, a machine translation dataset composed from a collection of various sources, including news commentaries and parliament proceedings.

### Libraries Used
- `transformers`: For utilizing and fine-tuning the Roberta-base model.
- `sacrebleu`: For evaluating the quality of machine translation outputs.
- `huggingface-hub`: For accessing the model and tokenizer from the Hugging Face model hub.
- `datasets`: For handling and processing the dataset.
- `numpy`: For numerical computations.
- `torch`: For building and training neural networks.

### Training Details
- **Pretrained Model**: Helsinki-NLP/opus-mt-en-ro
- **Weight Decay**: 0.01
- **Learning Rate**: 2e-5
- **Batch Size**: 16
- **Number of Epochs**: 3

### Results 

| Epoch | Training Loss | Validation Loss | Bleu     | Gen Len   |
|-------|---------------|-----------------|----------|-----------|
| 1     | No log        | 0.403127        | 26.665000| 33.886000 |
| 2     | 0.106500      | 0.407422        | 26.357100| 34.178000 |
| 3     | 0.106500      | 0.409481        | 26.344100| 34.093000 |

### Usage
```
from transformers import AutoModelForSeq2SeqLM

tokenizer = AutoTokenizer.from_pretrained("likhith231/opus-mt-en-ro-finetuned-en-to-ro")
model = AutoModelForSeq2SeqLM.from_pretrained("likhith231/opus-mt-en-ro-finetuned-en-to-ro")
text = "my name is likhith prudhivi"
inputs = tokenizer(text, return_tensors="pt").input_ids
outputs = model.generate(inputs, max_new_tokens=40, do_sample=True, top_k=30, top_p=0.95)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```
