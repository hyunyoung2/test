---
layout: post
title: A unified architecture for natural language processing- deep neural networks with multitask learning
subtitle: Title of paper - A unified architecture for natural language processing- deep neural networks with multitask learning
category: NLP papers - Multi-Task
tags: [neural network, multi task]
permalink: /2019/10/05/A_Unified_Archtecture_for_Natural_Language_Processing-_Deep_Neural_Networks_With_Multitask_Learning/
css : /css/ForYouTubeByHyun.css
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
  
---

This is a brief summary of paper named [A unified architecture for natural language processing: deep neural networks with multitask learning (Collobert	and Weston., ICML 2008)](https://dl.acm.org/citation.cfm?id=1390177)

This post is arranged for me to understand multi-task learning.


{% include MathJax.html %}

This paper focused on the multi-task in NLP, the portion of sharing between different task is look-up table for embedding. 

Their concept using look-up,Variation on Word Representation, is used for other feature like capitalization and relative position between each word and predicate.


![Collobert	and Weston. (2008)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Multi_Task/2019-10-05-A_Unified_Archtecture_for_Natural_Language_Processing_Deep_Neural_Networks_With_Multitask_Learning/Multi-Task1.jpg)


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They describe a single convolutional neural network architecture that, given a sentence, outputs a host of language processing predictions: part-of-speech tags, chunks, named entity tags, semantic roles, semantically similar words and the likelihood that the sentence makes sense (grammatically and semantically) using a language model. The entire network is trained jointly on all these tasks using weight-sharing, an instance of multitask learning. All the tasks use labeled data except the language model which is learnt from unlabeled text and represents a novel form of semi-supervised learning for the shared tasks.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://dl.acm.org/citation.cfm?id=1390177">The paper: A unified architecture for natural language processing: deep neural networks with multitask learning (Collobert	and Weston., ICML 2008)</a>
</div>

# Reference 

- Paper 
  - [ICML Version: A unified architecture for natural language processing: deep neural networks with multitask learning (Collobert	and Weston., ICML 2008)](https://dl.acm.org/citation.cfm?id=1390177)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
