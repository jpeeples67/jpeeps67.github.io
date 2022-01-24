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

<!-- <div class="section">
    <h5>Links</h5>
    <div class="container" style="width:95%"> -->

## Links
<!-- Icon row -->
<div class="row">
  <div class="two columns">
    <a href="https://arxiv.org/abs/2001.00215"><img style="border: 1px solid #ddd; border-radius: 4px; padding: 2px; width: 108px;" src="./images/arxiv.jpg"></a>
  </div>
  <div class="two columns">
    <a href="https://github.com/GatorSense/Histogram_Layer"><img style="border: 1px solid #ddd; border-radius: 4px; padding: 0px; width: 116px;" src="./images/code.png"></a>
  </div>          
  <div class="two columns">
    <a href="https://ieeexplore.ieee.org/document/9652037"><img style="border: 1px solid #ddd; border-radius: 4px; padding: 0px; width: 116px;" src="./images/ieee.jpg"></a>
  </div>    
  <div class="two columns">
    <a href="https://faculty.eng.ufl.edu/machine-learning/"><img style="border: 1px solid #ddd; border-radius: 4px; padding: 2px; width: 170px;" src="./images/logo.png"></a>
  </div>   
</div>
<!-- Link row -->
<div class="row">
  <div class="two columns">                  
    <a href="https://arxiv.org/abs/2001.00215">ArXiv Paper</a>
  </div>
              <div class="two columns">
    <a href="https://github.com/GatorSense/Histogram_Layer">Code</a>
  </div> 
<div class="two columns">
    <a href="https://ieeexplore.ieee.org/document/9652037">IEEE Paper</a>
  </div> 
<div class="two columns">
    <a href="https://faculty.eng.ufl.edu/machine-learning/">Lab</a>
  </div> 
</div>
<br>

    </div>
</div>