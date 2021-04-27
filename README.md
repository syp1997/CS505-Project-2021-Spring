# Neural Style Transfer

BU CS 585 Final Project - Spring 2021<br>Bowen Sun, Hao He, Yinpei Su, Zimou Sun<br>25th April 2021

## 1.Introduction

Neural style transfer is an optimization technique used to take two images—a content image and a style reference image (such as an artwork by a famous painter)—and blend them together so the output image looks like the content image, but “painted” in the style of the style reference image. 

This is implemented by optimizing the output image to match the content statistics of the content image and the style statistics of the style reference image. These statistics are extracted from the images using a convolutional network.

## 2.Method

#### 2.1 Style Transfer for Arbitrary Styles

Artistic style transfer may be defined as creating a stylized image x from a content image c and a style image s. Typically, the content image c is a photograph and the style image s is a painting. A neural algorithm of artistic style [9] posits the content and style of an image may be defined as follows:

- Two images are similar in content if their high-level features as extracted by an image recognition system are close in Euclidean distance.
-  Two images are similar in style if their low-level features as extracted by an image recognition system share the same spatial statistics.

The complete optimization objective for style transfer may be expressed as:

```text
<div  align="center">    
<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/loss1.png" alt="precision_recall" width = "40%" height="40%" align=center/>
</div>
```

<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/loss2.png" alt="precision_recall" width = "50%" height="50%" align=center />

#### 2.2 StarGAN v2

Let X and Y be the sets of images and possible domains, respectively. Given an image x, and an arbitrary domain y, the goal is to train a single generatorGthat can generate diverse images of each domain y that corresponds to the image x. They generate domain-specific style vectors in the learned style space of each domain and train G to reflect the style vectors. 

There are four modules: **Generator**, **Mapping network**, **Style encoder**, **Discriminator**. 

**Adversarial objective.**

<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/adv.png" alt="precision_recall" width = "50%" height="50%" align=center/>

**Style reconstruction.**

<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/sty.png" alt="precision_recall" width = "50%" height="50%" align=center/>

**Style diversification.**

<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/ds.png" alt="precision_recall" width = "50%" height="50%" align=center/>

**Preserving source characteristics.**

<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/cyc.png" alt="precision_recall" width = "50%" height="50%" align=center/>

**Full objective.**

<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/full.png" alt="precision_recall" width = "50%" height="50%" align=center/>

## 3.Data Collection

**CelebFaces Attributes Dataset (CelebA)** is a large-scale face attributes dataset with more than 200K celebrity images, each with 40 attribute annotations. We use these celebrity photos as content images. For Style Transfer for Arbitrary Styles, we use style images from tf-hub, and find some other style imagess from internet; for StarGanv2, we use the sample images of it as style images. After that, we also use our own images as content images to play with it.

## 4.Results

#### 4.1 Style Transfer for Arbitrary Styles

We choose several distinct styles and collect celebrity images, applying each style to these celebrity photos.

<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/res1.png" alt="precision_recall" width = "100%" height="100%" align=center/>

#### 4.2 StarGANv2

We apply StarGAN to these celebrity images to transfer semantic attributes, synthesizing images that reflect diverse styles of references including hairstyle, makeup and beard.

<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/stargan.png" alt="precision_recall" width = "100%" height="100%" align=center/>

## 5.Analysis

#### 5.1 Qualitative Metrics

For Style Transfer for Arbitrary Styles in 4.1, we found when the color change of style images is obvious, the the quality of the generated image is poor. Shown in the following figure, the columns of 3rd, 5th, 7th, the quatity is relatively low. For other cases, the stylized images looks well.

<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/low_qua.png" alt="precision_recall" width = "100%" height="100%" align=center/>

For StarGANv2 in 4.2, we found when there are some obstructions on the face, the quality is poor. Or when the height and width of the picture are very different, the quality of the synthesized picture is very low. Shown in the following figure, the imges of 1st, 6th, 7th columns are not satisfying. When the face is properly proportioned, the algorithm works weill.

<img src="https://github.com/syp1997/CS585-Project-2021-Spring/blob/main/imgs/low_qua_2.png" alt="precision_recall" width = "100%" height="100%" align=center/>

#### 5.2 Quantitative Metrics

We use content loss and style loss to evaluate the synthesized images. For 