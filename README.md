# Text Similarity

## Table of Contents
  * [Overview](#overview)
  * [Motivation](#motivation)
  * [Approach](#approach)
  * [Run](#run)
  * [Bug / Feature Request](#bug---feature-request)
  * [Technology Stack](#technology-stack)
  * [Credits](#credits)


## Overview
This project is a step to find out the similarity between two long articles. There are models such as BERT, SBERT that can provide state-of-the-art results. But, the length of the tokens in a sequence is limited to 512, that possess a problem in case of long statements. One has to truncate the article that has all potential reasons for the loss of information in the truncated words. Thus, a different approach is taken in order to minimize the data loss.

## Motivation
Text similarity has use-cases in various sorts of fields such as to find out the the similarity between two articles be it news, or some else to the user to save the user's time in reading the same articles again and again, it can also be used to find out the plagiarism.

## Approach
The problem is to find out the semantic textual similarity between the given two text articles in an unlabelled dataset. 

At first, data is cleaned by removing all the stopwords(and, a, the etc), applying contractions, applying lemmatization and stemming techniques so that the words like receiving and received will be transformed in its root form i.e receive. Also, the tweets are coverted into small letters so that words like Python and python would be treated as same word. Any non-alphabetical character is removed.

The nominal approach to finding out the textual similarity in the text is to find out the word embeddings for the text and thereafter, find out the difference between the two embeddings. This could be done using cosine similarity, euclidean distance, soft cosine similarity, etc. 

But in this case, instead of just statements, these are paragraphs, thus, the approach I have taken is to break down the paragraphs into chunks of sentences of length 200 in which the first fifty words is overlapped by the previous chunk’s sentence so that the embeddings could take into effect the previous context.

For word embeddings, I used sbert which provides us with state-of-the-art word embeddings. It is has used bert under the hood, but, just after the bert, it has a pooling layer and then cosine similarity in case of semantic textual similarity task otherwise a softmax function. Sbert is based upon siamese network architecture as both the sentences have the tied weights. 

After splitting the paragraphs, I took the cosine similarity of each embedded sentence of one paragraph with embedded sentences of the other paragraph and find the max between all the similarities. Suppose, if the first half of the paragraph is semantically similar to the last half of the other paragraph then this technique could be robust to that. Otherwise, in the normal way, the word embedding might lose the semantically same context in two paragraphs during cosine similarity.

## Run
After downloading the dataset from [here](https://drive.google.com/file/d/1wQTSNIVk2YRliPCbjavAerzosynNAGng/view?usp=sharing), open a google colab notebook and run the cells.


## Bug / Feature Request
If you'd like to request a new feature/approach, feel free to do so by opening an issue [here](https://github.com/Shubhamm097/Text-Similarity/issues/new). Please include the relevant reasons for the feature or approach.

## Technology Stack
1. Python
2. Cosine Similarity
3. SBERT Architecture
4. BERT Architecture


## Credits
- [SBERT Research Paper](https://arxiv.org/abs/1908.10084)

- [SBERT Documentation](https://www.sbert.net/)
