---
layout: single
header:
  #image: /assets/images/textrank/fig1.JPEG
  teaser: /assets/images/textrank/fig1.JPEG
title:  "Extractive Text Summary using TextRank "
breadcrumbs: true
share: false
#permalink: /hello/
#date:    2018-02-11 16:00:00 -6000
#date:   2015-11-17 16:16:01 -0600
#categories: jekyll update
toc: true

---

For someone familiar with NLP and Deep learning, the Seq2Seq models come first in mind when we talk about summarization. But the main issue with it is that it requires a significant amount of data and resources for training such networks. In this post, I'll cover TextRank which doesn't require any training at all.

#### Goals
The main purpose of this blog post is to provide an understanding of TextRank, which very intuitive way of summarizing the text. 

### Background
TextRank is a quite an old technique, it was originally published in 2004 but it still popular extractive summarization technique. It very easy to understand and does not require any training, and therefore commonly used as a baseline. In order to understand how text-rank works the sentences, I recommend going through my post on [Page-Rank](https://isarth.github.io/pagerank/). 


Before going through TextRank, let us first understand, what are the ways we can summarize a text. Mainly there are two ways:
###  Abstractive and Extractive summarization
<p align='center'>
<img src="/assets/images/textrank/fig1.JPEG">

</p>
* **Extractive**  : It is similar to highlighting, We pick relevant sentences from the document, that make up the summary. Techniques used for the extractive summarization are graph based methods like TextRank,LexRank.
* **Abstractive** : It is similar to reading the whole document and then making notes in our own words, that make up the summary. Techniques used for the abstractive summarization is the popular Seq2Seq LSTM networks or attention based models.

### Text Rank
Quoting from the paper *"TextRank – is a graph-based unsupervised method for keyword and sentence
extraction".* Because it is unsupervised ranking method, it does require any training and supervised data.<br/><br />
 Focusing only on the summarization or sentence extraction, basic intuition behind text-rank is that, we want to extract sentences that can cover a major part of the text or which are a lot similar to other sentences. And in order to extract them, we somehow need to rank them based on this similarity criteria, this is where Page-rank comes into the picture. It is used for ranking the sentences based on their similarity.

### Algorithm
<p align='center'>
<img src="/assets/images/textrank/fig2.JPEG">

</p>
* We construct a graph of sentences where each node is a represents a sentence and all the sentences are connected to each other by (directed on an undirected) edges. 
* The weight of the edge is equal to the similarity between the two sentences. And then we apply Page rank over the graph to rank the sentences. 
* Finally we select K top sentences that represent our summary.

Basically this is it. Nothing complex and still provides decent results.

### Sentence similarity

The weight of the edge is a value representing the similarity between the two sentences. Originally in the paper, it was calculated using a number of common words present in the sentence. In order to repress the selection of long sentences, the value is divided by the lengths of the sentences. <br/><br/>
Finally, given two sentences Si and Sj  , with a sentence being represented by the set of Ni words that appear in the sentence: Si = w1,w2,w3...wn the similarity of Si and Sj is defined as


<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
\begin{equation}
 Similarity(S_i,S_j)=\dfrac{| {w_k|w_k \epsilon{S_i} \space \& \space w_k \epsilon{S_j}| } }{log(|S_i|)+log(|S_j|)} 
\end{equation}

### Implementation of Text rank

In order to explain it I made a jupyter noteboook [Link](https://github.com/isarth/text_rank/blob/master/exp/text_rank.ipynb) or you can use sumy a python library that has already implemented it !!




