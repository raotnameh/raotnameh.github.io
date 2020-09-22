---
layout: page
title: My current research focus
---

- *Note1: I take automatic speech recogntion (ASR) as an example to explain, because that's how I stumbled upon these problems (biased present in this article). But the problems are same in any system which uses DL as a core module function to learn the probability distribution over the output. I'm sorry if some of you are not able to connect to the example. If you wish to get a basic idea what ASR is please look at my other [post](https://raotnameh.github.io/2019/01/07/ASR/) on ASR.*
- *Note2: Preliminary Experiments are done on ASR system.*


<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

## Introduction
Here I add updates on the experiments on my current research focus. You would be thinking, what is his resreach focus? TBH, it's nothing fancy but the insights I gained in my 2-3 years of AI journey. In this period I worked on several projects using deep learning (DL) on Speech and NLP related problems. While it was a nice feeling everytime I got a good accuracy or less word error rate (WER) in case of an ASR, I was really enjoying it (until it lasted....just kidding I still fell good everytime we get a better testing accuracy). This feeling led me to use DL here and there and everywhere. Anything you throw at me I'm gonna train a DL based model, that's how exhaustively I was applying it. I was really enjoying the *NOOB* feeling of knowing all about DL. All of this changed after I started testing the trained models on a real time testing examples. The WER I was so proud of dropped and in some cases it as as if the output was jsut better than random (the model was trained on majority of male voice samples and thus worked very poorly on female test samples). Now you would be thinking, which project he is talking about? Well, all of this happend when I was working on a speech recognition project in collaboration with Humonics global pvt. ltd. The system was to be built for realtime use cases and it did not work as expected (I did not fell good for sometime, the models I was so proud of let me down). All of this, led me to debug the models and go back to the basics of math behind the models. Which in turn led me to understand their **shortcomings** and why I was facing all those **problems** during the deployment, which I hope to overcome during my Ph.D. at IIITD. 

## Problems?
Without further ado, let me be formal and let you in the problems I'm trying to solve. So, what I propose is to train deep learning based system which are:
1. Invariant to nuisances/noise and different types of biases (gender, race) present in a training dataset and, 
2. Capable of learning robust probability distribution using small amounts of data.

Let's elaborate these 2 statement, I just made. 
* Firstly, If we can learn an invariant representation[^ref2],[^ref3], example w.r.t. to gender (male/female in case of an ASR system) then a model trained on a dataset which has majority of training examples male recordings the, we expect it to work as good as on female recordings. Let's take an another example, the task is to differentiate between different types of chairs. If we learn an invariant representaion w.r.t, to the different pose/orientations of the same chair, then the trained model would be more robust to different orientations of the input data(chairs in our case).
* Secondly, A model can learn robust representations given a specific task using a small dataset. If the dataset is free of unwanted nuisances and biases. I talk why is this true, [later in detail](#reason). Just to give a hint to the reader, it's because the input feature space is reduced.

## Solutions?
Let's talk about the possible solutions. 
* Firstly, We need to learn an invariant representation w.r.t to unwanted nuisances and biases (gender, accent in case of ASR or orientation/lighting in case of chair classification task) present in the dataset such that their is no or minimum loss of information from the input given teh main task (transcribing audios in case of an ASR or classifying the chairs). This can be achieved if we can learn a **masking fuction** in such a way to: 
    * Focus on retaining specific input features which are relevant for the specific task, thus achieving invariance to other subset input features or, 
    * Focus on removing[^ref1] specific input features which are not relevant for the task. (preliminary [experiments](#experimentations) using this approach are promising)
It is easier to tell a neural network what to remove from the input representation using adversarial forgetting[^ref1] than what not to. 

<a name="reason">
* Secondly, The same masking function can be used for different languages to remove these unwanted biases and nuisances (transfer learning). In the case of low resource languages/dataset, it would be instrumental.
</a>

We can think of the masking function as a preprocessing step before passing it to the main task, which masks out the unwanted nuisances and biases from the input space. My **current-research** focus revolves around answering/utilizing these directions in making DL based systems more robust to the problems I mentioned. 

## Experimentations 
All the Experiments are done with an assumption that transcribing a speech is the primary task and anything else is the secondary task (classifying the gender and accent of the speech utterance). Thus masking out the information required for the secondary task, which would not affect the primary task.

Architecture choice is based on this implementation[^ref1]. In place of a the predictor (speech recognition in our case) we use DS2[^ref4] module. The dataset used is CommonVoice verison 1[^data1]. word error rate (WER) metric is used to compare the results. 

Input        | WER   |
------------:|----------:
Normal       | -
Masked-input | -

## Importance to the DL reserach community?  
From my understanding, most of the current research in DL focuses on learning a probability distribution over an output (y) given an input dataset (x) using a neural network (NN) s.t., 
y = F(x); {F: NN},
given a loss and optimization function. 

In this optimization formulation, there is one major flaw; there is no restriction on what basis the underlying function is learning the distribution over an output. It might be possible that its decision depends on an unwanted subset of input features, thus inducing unwanted bias (gender) and, as a result, dependence on them. For example, in the case of speech recognition, it could associate the gender of the speakers, which is an unwanted dependence. Therefore, the system would work worse to a specific gender, which is seen less during training.
If we all agree that not all the input features may be relevant to a given task (ex: ASR). Then we can propose learning a mask function (M) given the input and the task. The mask is then applied to the input before passing it to the task-specific function for training. The masking function is learned in such a way that it achieves one of the solutions proposed before.

## Possible applications? 
The research direction that I am proposing can be applied to any existing DL based framework. For example,
1. The same masking function can be used for different languages to remove these unwanted biases and nuisances (transfer learning). In the case of low resource languages, it would be instrumental.
2. Explainability: High-risk, high stakes systems can be built robustly with easier explainability using this approach compared to standard end to end DL based systems.


### References
[^ref1]: [Invariant Representations through Adversarial Forgetting](https://arxiv.org/pdf/1911.04060.pdf) 
[^ref2]: [Learning Noise-Invariant Representations for Robust Speech Recognition](https://arxiv.org/pdf/1807.06610.pdf)
[^ref3]: [Invariant representation learning for robust deep networks](https://assets.amazon.science/ba/d7/902f6d6c4bd6812565e2b9eca667/invariant-representation-learning-for-robust-deep-networks.pdf)
[^ref4]: [Deep Speech 2: End-to-End Speech Recognition in English and Mandarin](https://arxiv.org/abs/1512.02595)
[^data1]: [CommonVoice version 1 dataset](https://common-voice-data-download.s3.amazonaws.com/cv_corpus_v1.tar.gz)

*Note: Preliminary Experiments are done on speech-based systems if any.*

