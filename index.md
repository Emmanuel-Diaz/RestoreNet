---
layout: page
title: Quantifying Image Restoration in World War II Photographs
description: Quantifying Image Restoration in World War II Photographs
author: Emmanuel Diaz
---
[Read the report here](https://github.com/Emmanuel-Diaz/DSC180B-Project/blob/master/DSC%20180B%20Report.pdf)

## Introduction
Image restoration is a field that has evolved tremendously, starting from signal processing techniques to modern day neural networks. The advent of big data makes neural networks stronger than ever before, and images are no exception to the influx of data. The latest research has left questions regarding the best way to learn from images to restore others.


It is widely known that old photos converted from film to digital might have experienced some degradation in the process. World War II photos are no exception and properly restoring these images will benefit us in preserving historical documents. I will investigate if using GANs to approach the ‘image inpainting’ problem, where sections of the image are occluded and we have to ‘fill in the blanks’, will give us not only a perceptual improvement in quality but also a quantification of how well the restoration occurred.
![Goal](/assets/project_goal.png)


## Data Collected
In order to understand the data population, I saved 3K images from [ww2db.com](https://ww2db.com/) and categorized them into 3 sections: Pre-War, Mid-War, Late-War

![Distribution](/assets/chart.png)


Utilizing a blob detector and using KMeans clustering with two simple features, I found two clusters within the data population.
![blob_scatter](/assets/blob_scatter.png)

Here is an example of images from each cluster.
![blob_detector](/assets/blob_detector.png)

The idea is to use images similar WWII images to the degraded image for training then evalute the performance.

## Methods
We create a mask along the degraded imperfections, we want these areas to be restored.
![Mask Process](/assets/mask_process.png)


## Results
I try to maximize my defined metric from the report. See here: [Report](https://github.com/Emmanuel-Diaz/DSC180B-Project/blob/master/DSC%20180B%20Report.pdf)

For the first test, we try **block inpainting** where a center block is inpainted and the 

<p align="center"><strong>Block Mask Untrained Model</strong></p>
![Random Gen](/assets/random_gen_img_sheet.jpg)
<p align="center">Metric: +6.9027</p>

<br>

<p align="center"><strong>Block Mask Group Trained Model</strong></p>
![Trained Gen](/assets/train_gen_img_sheet.jpg)
<p align="center">Metric: +11.59994</p>

<br>

Now we try **selective mask inpainting** where we pass a custom mask where the photo imperfections are
<p align="center"><strong>Selective Untrained Model</strong></p>
![Trained Gen](/assets/selective_mask_img_sheet.jpg)
<p align="center">Metric: +4.3359</p>

<br>

<p align="center"><strong>Selective Trained Model</strong></p>
![Trained Gen](/assets/selective_mask_trained_img_sheet.jpg)
<p align="center">Metric: +12.2342</p>

## Discussion

Through testing varying training groups and mask selections, it is clear that trained models perform better than untrained selections. However, group training gives similar performance to training over entire dataset. The best restoration occurred with the finest mask as the following:

![before_during_after](/assets/before_during_after.png)

Finer masking techniques assist in producing a better restoration, so localizing the regions is crucial. Training with WWII images seemed to tailor the inpainting in favoring similar color values, leading to better restoration.


## Conclusion

Image restoration is critical in preserving historical documents from degradation. In essence, it is crucial for methods to be developed in cases where photos get damaged, corrupted, or acquired poorly. We see that Generative Adversarial Networks have the potential to learn from domain data to improve image restoration. By using training data from the population of images you would like to restore, the network will have better efforts of learning such process. We have also seen that localizing degraded artifacts can improve restoration quality as well.
