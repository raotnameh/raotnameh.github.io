---
layout: page
title: My current research focus
---

<sup><sup> Note: I take automatic speech recogntion (ASR) as an example to explain, because that's how I stumbled upon these problems (biased present in this article). But the problems are same in any system which uses DL as a core module function to learn the probability distribution over the output. I'm sorry if some of you are not able to connect to the example. If you wish to get a basic idea what ASR is please look at my other [post](https://raotnameh.github.io/2019/01/07/ASR/) on ASR. </sup></sup>


Here I add updates on the experiments on my current research focus. You would be thinking, what is his resreach focus? TBH, it's nothing fancy but the insights I gained in my 2-3 years of AI journey. In this period I worked on several projects using deep learning (DL) on Speech and NLP related problems. While it was a nice feeling everytime I got a good accuracy or less word error rate (WER) in the case of an ASR system, I was really enjoying it (until it lasted....just kidding I still fell good everytime we get a better testing accuracy). This feeling led me to use DL here and there and everywhere. Anything you throw at me I'm gonna train a DL based model, that's how exhaustively I was applying it. I was really enjoying the *NOOB* feeling of knowing all about DL. All of this changed after I started testing the trained models on a real time testing examples (Which I was and I am still proud of...of course I'm talking about my trained models). The WER I was so proud of dropped and in some cases it as as if the output was random (the model was trained on male dominated voice samples and thus worked very poorly on female test recordings). Now you would be thinking, which project he is talking about? Well, all of this happend when I was working on a speech recognition project in collaboration with Humonics global pvt. ltd. The system was to be built for realtime use cases and it did not work as expected (I did not fell good for sometime, the models I was so proud of let me down in front of everyone). All of this, led me to debug the models and go back to the basics of math behind the models. Which in turn led me to understand their **shortcomings** and why I was facing all those **problems** during the deployment, which I hope to overcome during my Ph.D. at IIITD. 

Without further ado, let me be formal and let you in the problem I'm trying to solve. So, what I propose is to train deep learning based system which are:
1. Invariant to nuisances/noise and different types of biases (gender, race) present in a training dataset and, 
2. Capable of learning robust probability distribution using small amounts of data.

Let's elaborate these 2 statement, I just made. If we can learn an invariant representation w.r.t. to gender (male/female) then a model trained on a dataset which has training examples which are male 
Solutions: 
Both of these can be achieved if we can somehow tell a neural network to learn a masking function in such a way to:
Focus on retaining specific input features which are relevant for the specific task, thus achieving invariance to other subset features or, 
Focus on removing specific input features which are not relevant for the task. (preliminary results are promising)
It is easier to tell a neural network what to remove from the input representation using adversarial forgetting than what not to. 

My current research focus revolves around answering/utilizing these directions in making DL based systems more robust to the problems I mentioned. 

Importance to the field:  
From my understanding, most of the current research in DL focuses on learning a probability distribution over an output (y) given an input dataset (x) using a neural network (NN) s.t., 
y = F(x); {F: NN},
given a loss and optimization function. 

In this optimization formulation, there is one major flaw; there is no restriction on what basis the underlying function is learning the distribution over an output. It might be possible that its decision depends on an unwanted subset of input features, thus inducing unwanted bias (gender) and, as a result, dependence on them. For example, in the case of speech recognition, it could associate the gender of the speakers, which is an unwanted dependence. Therefore, the system would work worse to a specific gender, which is seen less during training.
If we all agree that not all the input features may be relevant to a given task (ex: ASR). Then we can propose learning a mask function (M) given the input and the task. The mask is then applied to the input before passing it to the task-specific function for training. The masking function is learned in such a way that it achieves one of the solutions proposed before.

Applicability to Facebook: 
The research direction that I am proposing can be applied to any existing framework. For example,
The same masking function can be used for different languages to remove these unwanted biases and nuisances (transfer learning). In the case of low resource languages, it would be instrumental.
Explainability: High-risk, high stakes systems can be built robustly with easier explainability using this approach compared to standard end to end DL based systems.



For more details: https://raotnameh.github.io/current_rf/

Note: Preliminary Experiments are done on speech-based systems if any.


