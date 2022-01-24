---
layout: single
title: "Histogram Layers for Texture Analysis"
date: 2022-01-23
tags: [deep learning, histograms, image classification, texture analysis]
---

## Problem Statement: Shortcomings of Convolutional Neural Networks
Convolutional neural networks (CNN) have been vital for a variety of applications. Despite the innovations of CNN, these models are great at **structural** textures but not **statistical** textures. To illustrate this point, below is an example of different structural and statistical textures:
![Texture](/images/Textures.PNG)
<br/>We can visually see the distinct differences between the different texture combinations. The structural textures are a checkboard, cross, and stripe while the statisistical textures are pixels sampled from multinomial, binomial and constant distributions. A CNN could easily distinguish the structural textures, but would struggle with the statistical texures. 

### Why would a CNN struggle with statistical textures?
Structural texture approaches consist of defining a set of texture examples and an order of spatial positions for each exemplar [(Materka et al., 1998)](https://www.researchgate.net/profile/Andrzej-Materka/publication/249723259_Texture_Analysis_Methods_-_A_Review/links/02e7e51ef8d539a9da000000/Texture-Analysis-Methods-A-Review.pdf). Convolution is a weighted sum operator that uses spatial information to learn local relationships between pixels. Given enough samples from each distribution, the mean values are approximately the same and outputs from a convolution will be similar as shown:
![Example convolution outputs](/images/Sampling.gif)
![Distribution Images](/images/Distributions.JPG)
<br/>The average operation is a special case of convolution where the all of the weights are equal to 1/number of data points. As a result, the CNN will struggle to capture a linear combination of pixels that learns the statistical information of the data (*i.e.*, cannot learn weights to discriminate statistical exemplars). Here is an example where if a 3 by 3 convolution is used, the model can easily learn weights to tell the cross and checkboard apart. However, if we sample from a different distribution and retain the same shape, a convolution operation cannot learn weights to distinguish this change as the convolution is unable to account for individual pixel intensity changes.
![CNN_Failure](/images/CNN_Failure.PNG) 

<br/>In order to capture the statistical textures, instead of understanding the structure of each texture, the data can be represented through parameters that characterize the distributions and correlation between the intensity and/or feature values in an image [(Humeau-Heurtier, 2019)](https://ieeexplore.ieee.org/abstract/document/8600329).

## Method: Histogram Layer
The proposed solution is a **local** histogram layer. Instead of computing global histograms as done previously, the proposed histogram layer directly computes the local, spatial distribution of features for texture analysis, and parameters for the layer are estimated during backpropagation. Histograms perform a counting operation for values that fall within a certain range. Below is an example where we are counting the number of 1s, 2s, and 3s in local windows of the image:
![Local_Hist](/images/Stand_Hist.gif)
<br/> The standard histogram operation is not differentiable; however, a smooth approximation (*i.e.*, radial basis function) can be used instead as shown below:
![Local_RBF](/images/RBF_Hist.gif)
<br/> Another advantage of the proposed method is that the histogram layer is easily implemented using pre-exisiting layers! Any deep learning framework (*e.g.*, Pytorch, TensorFlow) can be used to integerate the histogram layer into deep learning models.
![Implementation](/images/Implementation.png)

## Applications of Histogram Layer
There are several real-world applications for the histogram layer! Examples include the health domain and remote sensing tasks such as disease detection and crop quality management ([Image Source](https://www.letsnurture.com/blog/using-deep-learning-for-image-based-plant-disease-detection.html )).<br/>
![Plants](/images/Disease_detection.jpg)

## Check Out the Code and Paper!
This [work](https://ieeexplore.ieee.org/document/9652037) was accepted to the **IEEE Transactions on Artificial Intelligence**! Our [code](https://github.com/GatorSense/Histogram_Layer) and [paper](https://arxiv.org/abs/2001.00215) are available! 

## Citation

### Plain Text:

J. Peeples and W. Xu and A. Zare, "Histogram Layers for Texture Analysis," 
in IEEE Transactions on Artificial Intelligence, DOI 10.1109/TAI.2021.3135804, 2021.

### BibTex:

@Article{Peeples2021Histogram,<br>
Title = {Histogram Layers for Texture Analysis},<br>
Author = {Peeples, Joshua and Xu, Weihuang  and Zare, Alina},<br>
Journal = {IEEE Transactions on Artificial Intelligence},<br>
Volume = {},<br>
Year = {2021},<br>
number={}<br>
pages={1-1}<br>
doi={10.1109/TAI.2021.3135804}}


## Links
<!-- [![alt text](image link)](web link) -->
[![ArXiv Paper][1]][2]{:height="36px" width="36px"}[![Github Repositor][3]][4]{:height="36px" width="36px"}[![IEEE Paper][5]][6]{:height="36px" width="36px"}[![Lab][7]][8]{:height="36px" width="36px"}

[1]: /images/arxiv.jpg
[2]: https://arxiv.org/abs/2001.00215
[3]: /images/code.png
[4]: https://github.com/GatorSense/Histogram_Layer
[5]: /images/ieee.jpg
[6]: https://ieeexplore.ieee.org/document/9652037
[7]: /images/logo.png
[8]: https://faculty.eng.ufl.edu/machine-learning

<!-- [![ArXiv Paper](/images/arxiv.jpg"ArXiv Paper")](https://arxiv.org/abs/2001.00215)
[![Github Repository](/images/code.png"Code")](https://github.com/GatorSense/Histogram_Layer)
[![IEEE Paper](/images/ieee.jpg"IEEE Transactions on AI Paper")](https://ieeexplore.ieee.org/document/9652037)
[![Lab](/images/logo.png"GatorSense Lab Website")](https://faculty.eng.ufl.edu/machine-learning) -->



