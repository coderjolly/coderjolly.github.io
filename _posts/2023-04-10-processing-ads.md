---
layout: post
title:  "Processing Image Advertisements for Contextual Analysis"
date:   2023-04-10
title_include: true
categories: writing
image_url: ""
---

<style>body {text-align: justify}</style>

Promotion of products is now a common practice and is heavily controlled by broadcasting of advertisements. Image based advertisements are still one of the best ways to promote products but it is painstakingly difficult to personalize the content for the target audience and covey the sentiments. It is proven that an image can be perceived in different manners and hence different emotions can be conveyed via them. 

<figure>
<img src="/assets/img/image-advertisements/broken_classifier.jpeg" width=650 style="display: block; margin: 0 auto">
</figure>


This study tries to compare three backbone deep learning architectures namely, ResNet 50, MobileNetv3 Large and EfficientNet B3 on an image advertisement dataset to classify the underlying sentiments being perceived by the consumers. Transfer learning is used to deal with the issue of a small dataset when brought down to the usable contexts after data processing.

## Dataset Used

We have used a publicly available dataset developed by the combined efforts of Hussain et al. at the University of Pittsburgh with over 64,000 advertisement images and over 3,000 video advertisements. The authors used Amazon Mechanical Turk workers to tag each advertisement to its respective topic (eg. category of the product the advertisement targets) and what sentiment it conveys to the viewer (eg. how plants/trees play a vital role in sustenance) followed by what method it uses to imbibe that message (eg. the presence of trees or plants might be depicting life). The approach used to gather and annotate this data was influenced by the research in Media
Studies, an academic field that examines the content of mass media messages, with input from one of the research paper authors who had formal education in the field. The data is accessible [here.](http://www.cs.pitt.edu/kovashka/ads/)

![dataset](/assets/img/image-advertisements/dataset.png)

## Methodology

Before training, the images were analysed to come up with a pre-processing pipeline to denoise the images and improve their quality as most of the images were highly compressed.

<ol type="A">
 <li><b>Bilateral Filter</b></li>
For improving the quality of the images, a smoothing filter for images had to be employed. So, a bilateral filter was used to reduce noise while preserving edges in a non-linear manner. It is quintessential to know that all other filters smudge the edges, while Bilateral Filtering retains
them.

![ads-bilateral](/assets/img/image-advertisements/ads-bilateral.png)

 <li><b>Pre-processing Techniques</b></li>
Pytorch provides various functional transformations that
can be applied using the torchvision.transform module. But, they require a parameter such as a factor by which an image can be transformed, therefore they cannot be applied to all images with the same factor. 

Five random images have been selected and functional image processing techniques like hue transforms, gamma transforms, solarize transformations, sharpness, etc have been applied to reach a conclusion that all images bearing uniqueness in their characteristics respond differently to functional transformations applied.

![pre-processing](/assets/img/image-advertisements/pre-processing.png)
 
 <li><b>Architectures</b></li>
Different backbone architectures were chosen to ensure
that different types of Convolution blocks were tested for the advertisement data. <b>Resnet-50</b>, <b>MobileNet V3 Large</b> and <b>EfficientNet B3</b> were chosen finally.

<table>
        <tr>
            <th> Architecture </th> <th> Params (Mil.)</th> <th> Layers </th> <th> GFLOPS </th> <th> Imagenet Acc. </th>
        </tr>
        <tr>
            <th> MobileNet V3 Large </th> <td class="r"> 5.5 </td> <td> 18  </td> <td> 8.7 </td> <td class="r"> 92.57 </td>
        </tr>
        <tr>
            <th> EfficientNet B3 </th> <td> 12.2 </td> <td> 29  </td> <td> 1.83 </td> <td> 96.05 </td>
        </tr>
        <tr>
            <th> Resnet-50 </th> <td> 25.6 </td> <td> 50  </td> <td> 4.09 </td> <td> 95.43 </td>
        </tr>
</table>
</ol>

<hr class="slender">

## Results

The dataset used in this study presented the the multiclass, multilabel classification problem. Thus, to make the model predict multiple labels, a sigmoid layer had to be added before the loss function to get 0 or 1 prediction for all the classes of the data. To achieve this, the BCEWITHLOGITSLOSS function of PyTorch was used as it combines the Sigmoid layer and the binary cross entropy loss function in one single class. This makes theses operations more numerically stable than their separate counterparts.

The pre-trained weights were chosen to be the IMAGENET1K V2 weights and only the last classification layer was fine-tuned. The rationale behind performing this type of shallow-tuning was that the Imagenet data is very similar to the advertisement images in our dataset. Additionally, the size of the selected dataset is small so deep-tuning might not work well.

![f1&loss_plots](/assets/img/image-advertisements/f1&loss_plots.png)

<table>
        <tr>
            <th> Model </th> <th> F1 Score </th> <th> Time </th> <th> F1 epochs </th> <th> Loss Epochs </th>
        </tr>
        <tr>
            <th> MobileNet V3 Large </th> <td class="r"> 0.168 </td> <td> 80s  </td> <td> 50 </td> <td class="r"> 98 </td>
        </tr>
        <tr>
            <th> EfficientNet B3 </th> <td> 0.189 </td> <td> 153s  </td> <td> 5 </td> <td> 90 </td>
        </tr>
        <tr>
            <th> Resnet-50 </th> <td> 0.179 </td> <td> 50s  </td> <td> 10 </td> <td> 0 </td>
        </tr>
</table>

The best model which in this case was the **EfficientNet B3** model was used to do further analysis like visualizing the trained filters and using Grad-CAM to understand which areas of the image the model focused on to generate the predictions.

## Observations

Looking at the above table it can be seen that the MobileNet architecture was the fastest to train per epoch. It took less time per epoch but, if number of epochs required to converge is considered, it does not train the fastest.

The lowest validation set loss for ResNet was at epoch 0. This means that the model started overfitting right after the first epoch in terms of the loss. However, it took 10 epochs to converge on the F1 score.

EfficientNet model performed the best in terms of the overall F1 score on the test set. Another surprising observation is that the EfficientNet model takes the longest to train per epoch even though the number of trainable parameters is nowhere close to ResNet.

![confusion-matrix](/assets/img/image-advertisements/confusion-matrix.png)

In the above figure,  it can be seen that the model classifies the labels Fashionable, Feminine, and Eager the best which are the classes that have the most number of training examples. This shows that if we increase the training dataset size, the models could improve a lot.

## Grad-CAM Visualizations

As the EfficientNet B3 model produced the best F1 score on the test set, it was used to generate the GradCAM visualizations to understand the model outputs.

![first-layer-gradcam](/assets/img/image-advertisements/first-layer-gradcam.png)

We can see from the above figure that in the first layer of the network the model identifies prominent edges of the image. We can confirm this by looking at the filters of the first layer. Most of the filters look like they identify edges and corners.

![second-layer-gradcam](/assets/img/image-advertisements/second-layer-gradcam.png)

In the middle layer of the network, the model is looking at many different features but isn’t looking at the most relavant features for that label. 

![third-layer-gradcam](/assets/img/image-advertisements/third-layer-gradcam.png)

And lastly, in the final layer of the network, the model looks only at the relavant features of the image depending on the current label. For example, here it is focusing on the player playing football for the ’Active’ label.

## Conclusion

Visually looking at the gradcam visualizations and the predictions it is clear that the model is performing much better than what the F1 scores show. 

The low performance of the models in this study can be attributed to the low quality of the labels along with a lack of available training data. Even though the convolutional layers of the EfficientNet model were not fine-tuned, it was observed that the model could find relavant features in the image depending on the label. 

This shows that transfer learning is a powerful tool to train models and reduce turn-around times. Transfer learning enables the use of deep learning models even when the amount of available data is very less.
