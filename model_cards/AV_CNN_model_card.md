---
COMP34812 Authorship Verification CNN with BERT Embeddings
---
language: en

license: cc-by-4.0

tags:
- text-classification
- bert-embeddings
- CNN
- authorship-verification

repo: https://github.com/elliot-brooks/nlu-coursework

---

# Model Card for w06148eb-a87068lp-AV

<!-- Provide a quick summary of what the model is/does. -->

This is a binary classification model that reads 2 inputs, and outputs if the texts were written by the same author. The model uses pre-generated BERT embeddings in a convolutional neural network (CNN). The outputs of the model were:
- Accuracy: 58.983333333333334
- Precision:  61.544920235096555
- Recall:  48.68814347392893
- F-score:  54.36677174114594

The model is inspired by 'Sentiment Analysis of Text Reviews Using Lexicon-Enhanced Bert Embedding (LeBERT) Model with Convolutional Neural Network' and it's use of BERT embeddings with a CNN based model.
                        
Mutinda James, Waweru Mwangi, and George Okeyo. 2023. "Sentiment Analysis of Text Reviews Using Lexicon-Enhanced Bert Embedding (LeBERT) Model with Convolutional Neural Network" Applied Sciences 13, no. 3: 1445. https://doi.org/10.3390/app13031445

## Model Details

### Model Description

<!-- Provide a longer summary of what this model is. -->

The model uses the embeddings from distilbert-base-uncased, and performs pairwise analysis on 2 inputs to verify if they were written by 2 authors.

The model is intended to directly compare 2 texts of up to 256 tokens per input, for a total max length of 512 between both inputs.

The pipeline first pre-processes then conjoins the training inputs with the specified '[SEP]' token between them. The embeddings for the texts are then generated with a distilbert tokenizer, and then used to train a 11 layer model, including 2 convolution layers and 2 pooling layers, creating a CNN architecture.

- **Developed by:** Elliot Brooks and Liam Patterson
- **Language(s):** English
- **Model type:** Supervised
- **Model architecture:** CNN
- **Finetuned from model [optional]:** N/A

### Model Resources

<!-- Provide links where applicable. -->

- **Repository:** N/A
- **Paper or documentation:** https://www.mdpi.com/2076-3417/13/3/1445

## Training Details

### Training Data

<!-- This is a short stub of information on the training data that was used, and documentation related to data pre-processing or additional filtering (if applicable). -->

30K pairs of texts drawn from emails, news articles and blog posts.

### Training Procedure

<!-- This relates heavily to the Technical Specifications. Content here should link to that section when it is relevant to the training procedure. -->

#### Training Hyperparameters

<!-- This is a summary of the values of hyperparameters used in training the model. -->


      - learning_rate: 5e-05
      - train_batch_size: 32
      - eval_batch_size: 32
      - seed: N/A
      - num_epochs: 100

#### Speeds, Sizes, Times

<!-- This section provides information about how roughly how long it takes to train the model and the size of the resulting model. -->


      - overall training time: 130s
      - duration per training epoch: 1s
      - model size: 9.28MB

## Evaluation

<!-- This section describes the evaluation protocols and provides the results. -->

### Testing Data & Metrics

#### Testing Data

<!-- This should describe any evaluation data used (e.g., the development/validation set provided). -->

A subset of the development set provided, amounting to 2K pairs.

#### Metrics

<!-- These are the evaluation metrics being used. -->
      - Precision
      - Recall
      - F1-score
      - Accuracy

### Results

The model obtained an F1-score of 54% and an accuracy of 59%.

## Technical Specifications

### Hardware
      - RAM: at least 32 GB
      - Storage: N/A,
      - GPU: V100 Premium (High RAM)

### Software
      - Transformers 4.40.0
      - Tensorflow 2.15.0
      - Torch 2.2.1+cu121

## Bias, Risks, and Limitations

<!-- This section is meant to convey both technical and sociotechnical limitations. -->

Any inputs (concatenation of two sequences) longer than 512 subwords will be truncated by the model.

## Additional Information

<!-- Any other information that would be useful for other people to know. -->

The hyperparameters were determined by experimentation with different values. 