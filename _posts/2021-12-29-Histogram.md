---
layout: single
title: "Histogram Layers for Texture Analysis"
date: 2021-12-29
tags: [feature learning, texture classification, histograms]
---

## Introduction: What is Texture?
There are no agreed definitions in the computer vision literature (cite). However, for texture, characterizing the spatial 
distribution of intensity and/or feature values is important.

## Problem Statement: Shortcomings of Convolutional Neural Networks
Convolutional neural networks have been vital for a variety of applications. Despite the innovations of CNN, these models are great at **structural** textures but not **statistical** textures. To illustrate this point, below is an example of different structural and statistical textures:
![Texture](/images/Textures.PNG)
We can visually see the distinct differences between the different texture combinations. The structural textures are a checkboard, cross, and stripe while the statisistical textures are pixels sampled from multinomial, binomial and constant distribution. A CNN could easily distinguish the structural textures, but would struggle with the statistical texures. Convolution is simply a weighted average operator. In the example above, the mean values are approximately the same. In order to capture the statistical textures, a model will need to learn the full distribution. 

## Method: Histogram Layer
The proposed solution is a **local** histogram layer. Instead of computing global histograms as done previously, the proposed histogram layer directly computes the local, spatial distribution of features for texture analysis, and parameters for the layer are estimated during backpropagation. The standard histogram operation is not differentiable; however, a smooth approximation (*i.e.*, radial basis function) can be used instead as shown below:
![Local_RBF](/images/Local_RBF.gif)
Another advantage of the proposed method is that the histogram layer is easily implemented using pre-exisiting layers! Any deep learning framework (*e.g.*, Pytorch, TensorFlow) can be used to integerate the histogram layer into any framework.
![Implementation](/images/Implementation.png)

## Applications of Histogram Layer
There are several real-world applications for the histogram layer! Examples include the health domain and remote sensing tasks such as disease detection and crop quality management ([Image Source](https://www.letsnurture.com/blog/using-deep-learning-for-image-based-plant-disease-detection.html )).
![Plants](/images/Disease_detection.jpg)

## Check Out the Code and Paper!
This [work](https://ieeexplore.ieee.org/document/9652037) was accepted to **IEEE Transactions on Artificial Intelligence**! Our [code](https://github.com/GatorSense/Histogram_Layer) and [paper](https://ieeexplore.ieee.org/document/9652037) are available! 

