---
layout: post
title:  "Lung Disease Classification"
date:   2022-12-30
title_include: true
categories: writing
image_url: ""
---

<style>body {text-align: justify}</style>

Chest X-rays scans are among the most accessible ways to diagnose lung diseases. This study tries to compare the detection of lung diseases using these scans from  three different datasets using deep neural networks. Three different backbone architectures, ResNet34, MobileNet V3 Large and EfficientNet B1 were used along with a set of models trained using transfer learning. It is observed that MobileNet takes the least amount of time to train while ResNet converges the fastest. Also, EfficientNet performs the best most of the times on Chest X-ray scans. An F1 score of 0.8 for the pneumonia dataset was obtained, 0.98 for the COVID-19 dataset and 0.46 for the multilabel chest X-ray 8 dataset. Finally, models are visualized using t-SNE and gradCAM to understand the features learned by the models and correlate them with the actual effect of the diseases on the lungs.

## Dataset Used
We have choosen 3 types of chest X-Ray datasets (Tab. 1) that have varying disease types to ensure that our models are robust. The
main concern while selecting the datasets was the number of images per class as most datasets were highly skewed. We rejected datasets where the images were compressed and noisy as this can lead to mis-diagnosis. This will help reduce the time spent in the pre-processing stage. The dataset links are as follows:
- Dataset 1 - <a href="https://www.kaggle.com/datasets/tolgadincer/labeled-chest-xray-images">Kaggle Link</a>
- Dataset 2 - <a href="https://www.kaggle.com/datasets/tawsifurrahman/covid19-radiography-database">Kaggle Link</a>
- Dataset 3 - <a href="https://www.kaggle.com/datasets/nih-chest-xrays/data">Kaggle Link</a>

A sample of the dataset can be downloaded from the following [link](https://drive.google.com/file/d1OpvSkIDzOlJUSCLJ-wfXSVsBbfhntun4/view?usp=sharing)

| Dataset                 | No. of Images                | Classes | Image Size  |
|-------------------------|------------------------------|---------|-------------|
| Dataset 1 (COVID)       | `10k:3.6k:1.3k`              | `3`     | `299x299`   |
| Dataset 2 (PNEUMONIA)   | `3k:1.5k:1.5`                | `3`     | `224x224`   |
| Dataset 3 (Chest Xray8) | `25k:12k:6k:5k:3k:2.7k:2.6k` | `7`     | `1024x1024` | 

![sample-dataset](/assets/img/chest-x-ray/sample-dataset.png)

## Methodology
In this study, 12 models, four for each of the three datasets will be trained. The first three models will be trained from scratch and the fourth model will be trained using transfer learning. The hyperparameters will be fixed across models to produce comparable results. Next, hyperparameters will be tuned to find the best model. Finally, the models will be visualized using t-SNE and Grad-CAM to explain model results. 

<ol type="A">
<li><b>Pre-processing Techniques</b></li>
 Before training, the images were analysed to come up with pre-processing techniques such as <b>Histogram Equalization</b> and <b>Gaussian Blur</b> with a 5x5 kernel as <a href="https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0265949" target="_blank" >Giełczyk et al.</a> showed that this improved the F1 score by 4% for chest X-ray classification. Visually, the contrast of the scan improved and allowed irregularities to stand out as shown in the figure below.

<figure>
<img src="/assets/img/chest-x-ray/histogram-equilization.png" width=750 height=250>
</figure>

<li><b>Data Augmentation</b></li>
During training, the scans were augmented using RandomAdjustSharpness and RandomAutocontrast in Pytorch to increase the number of images the model gets
to learn from and ensure that the model is robust to scans from different machines. RandomHorizontalFlip was also used to make the models invarient to the direction
of the scan as some scans were anterior-posterior while others were posterior-anterior.

<li><b>Architectures</b></li>
Different backbone architectures were chosen to ensure that different types of Convolution blocks were tested for the advertisement data. <b>Resnet-34</b>, <b>MobileNet V3 Large</b> and <b>EfficientNet B1</b> were chosen finally.

<!-- <div class="table-wrapper"> -->
<table>
        <tr>
            <th> Architecture </th> <th> Params (Mil.)</th> <th> Layers </th> <th> FLOPS (Bil.) </th> <th> Imagenet Acc. </th>
        </tr>
        <tr>
            <th> MobileNet V3 Large </th> <td class="r"> 5.5 </td> <td> 18  </td> <td> 8.7 </td> <td class="r"> 92.6 </td>
        </tr>
        <tr>
            <th> EfficientNet B1 </th> <td> 7.8 </td> <td> 25  </td> <td> 25.8 </td> <td> 94.9 </td>
        </tr>
        <tr>
            <th> Resnet-34 </th> <td> 21.8 </td> <td> 34  </td> <td> 153.9 </td> <td> 91.4 </td>
        </tr>
</table>
<!-- </div> -->

</ol>

<br/>

<hr class="slender">

## Experimental Setup

First undersampling was performed on the datasets. Then, the scans were preprocessed using histogram equalization and Gaussian blur before resizing them and storing them in separate directories to make it easier for PyTorch dataloaders. Two datasets in this study presented the multiclass classification problem while the third, chest X-ray 8 dataset presented the multiclass, multilabel classification problem. Thus, the training methodology was separated for these two problems. For the multilabel problem, a softmax layer had to be added before the loss function to get 0 or 1 prediction for all the classes of the data. For this, the BCEWITHLOGITSLOSS function of PyTorch was used as it combines the Sigmoid layer and the BCELoss function in one single class. This makes theses operations more numerically stable than their separate counterparts.

The backbone architectures were obtained directly from the torchvision library and the final classification layer was modified for the selected datasets. For the models which had to be trained from scratch, the weights were randomly initialized and the entire model was trained for a total of 100 epochs each. For the transfer learning models, the weights were initialized with the IMAGENET1K_V2 weights but the entire model was fine-tuned. The rationale behind performing deep-tuning was that the Imagenet data is very different from chest X-ray scans thus the model would need to learn features from Xray scans.

![f1&loss_plots](/assets/img/chest-x-ray/f1&loss_9_plots.png)

The above figure represents `Train & Val, F1 & Loss plots for the 9 models`. Initial training runs of the multilabel data produced a zero F1 score due to its highly imbalanced nature. To mitigate this, class wise weights were calculated and used with the loss function. This improved the F1 score considerably. Finally, the best models from each run by validation loss were used to get the test set metrics that are displayed in the tabel below.

<table>
        <tr>
            <th>Model</th>
            <th colspan="3" class="cmid">Resnet</th>
            <th colspan="3" class="cmid">Mobilenet</th>
            <th colspan="3" class="cmid">EfficientNet</th>
        </tr>
        <tr>
            <th>Dataset</th>
            <th>F1 Score</th>
            <th>Time</th>
            <th>Epoch</th>
            <th>F1 Score</th>
            <th>Time</th>
            <th>Epoch</th>
            <th>F1 Score</th>
            <th>Time</th>
            <th>Epoch</th>
        </tr>
       <tr>
         <th> Pneumonia </th>
         <td> 0.784 </td>
         <td> 82 </td>
         <td> <b> 22 </b> </td>
         <td> <b> 0.804 </b> </td>
         <td> <b> 75 </b> </td>
         <td> 42 </td>
         <td> 0.768 </td>
         <td> 110 </td>
         <td> 44 </td>
      </tr>
      <tr>
         <th> COVID </th>
         <td> 0.959 </td>
         <td> 50 </td>
         <td> <b> 21 </b> </td>
         <td> <b> 0.967 </b> </td>
         <td> <b> 37 </b> </td>
         <td> 44 </td>
         <td> <b> 0.979 </b> </td>
         <td> 56 </td>
         <td> 46 </td>
      </tr>
      <tr>
         <th> X-Ray 8 </th>
         <td> 0.411 </td>
         <td> 11,502 </td>
         <td> <b> 19 </b> </td>
         <td> <b> 0.406 </b> </td>
         <td> <b> 7,275 </b> </td>
         <td> 42 </td>
         <td> <b> 0.445 </b> </td>
         <td> 13,820 </td>
         <td> 31 </td>
      </tr>
    </table>

## Results Analysis

&#8226; It is clear that going from a smaller architecture to a bigger architecture, makes the model start to overfit earlier. The MobileNet model was the most unstable among the three and also took more epochs to reach the minima. The **EfficientNet** algorithm performs best for the COVID and Chest X-ray 8 dataset and all three architectures performed similar for the pneumonia dataset. This shows that the compound scaling of EfficientNet gives good results for chest X-ray data. <br/>
&#8226; The X-ray 8 dataset performed the worst among the three datasets which could be due to the high number of classes, class imbalance and the multilabel nature of the problem. Surprisingly, the pneumonia dataset performed worse than the COVID + pneumonia dataset which indicates that COVID cases are easier to distinguish from pneumonia cases. <br/>
&#8226; It can be seen that the MobileNet architecture was the fastest to train per epoch. It consistantly took less time per epoch but, if number of epochs required to converge is considered, it does not train the fastest all the time. It is also evident that ResNet converged the fastest at half the number of epochs compared with other models. <br/>
&#8226; EfficientNet models perform the best in terms of the overall F1 score on the test set with the exception of the Pneumonia dataset where surprisingly MobileNet performed the best.

<hr class="slender">

## Transfer Learning

As **EfficientNet** gave the best for COVID and chest X-ray 8 dataset, it was chosen for transfer learning. The model was trained from scratch with ImageNet weights and was applied for classification on the COVID, Pneumonia and Chest X-ray 8 datasets. 

![f1&loss_plots](/assets/img/chest-x-ray/f1&loss_transfer_plots.png)

<table>
        <tr>
            <th>Model</th>
            <th colspan="3">EfficientNet-Transfer Learning</th>
        </tr>
        <tr>
            <th>Dataset</th>
            <th>F1 Score</th>
            <th>Time</th>
            <th>Epoch</th>
        </tr>
        <tr>
            <th> Pneumonia </th>
            <td> 0.782 </td>
            <td> 114 </td>
            <td> 70 </td>
        </tr>
        <tr>
            <th> COVID </th>
            <td> 0.978 </td>
            <td> 56 </td>
            <td> 43 </td>
        </tr>
        <tr>
            <th> X-Ray 8 </th>
            <td> <b> 0.457 </b> </td>
            <td> 13,813 </td>
            <td> 29 </td>
        </tr>
</table>

The above figure represents `Train & Val, F1 & Loss plots for the 3 transfer learning models`. It can be seen that the transfer learning model had a much better start than the randomly initialized model. It also converged much quicker than the model trained from scratch. For the Pneumonia dataset, the model trained from scratch was highly unstable at the start and could not catch up to the transfer learning model even after 100 epochs in terms of the F1 score. The results are shown in the table below.

## Observations

The transfer learning models converged quicker than the other models with the exception of the Pneumonia dataset. Another observation is that the EfficientNet model takes the longest to train per epoch even though the number of trainable parameters is nowhere close to ResNet.

Also, MobileNet isn’t as fast to train as expected when compared to ResNet even though it has 4 times the learnable paramenters. This could be due to two reasons, depthwise convolutions are not optimized in the version of PyTorch and
CUDA used and training is getting CPU bound due to the data augmentation before each training run which would take the same amount of time for all the models.

<hr class="slender">

### T-SNE and Confusion Matrices

The figures below represent `T-SNE and Confusion matrices for the test set of the Pneumonia dataset`.

![t-sne-resnet-pneumonia](/assets/img/chest-x-ray/t-SNE-Resnet-pneumonia.png)

![t-sne-mobilenet-pneumonia](/assets/img/chest-x-ray/t-SNE-MobileNet-pneumonia.png)

![t-sne-efficientnet-pneumonia](/assets/img/chest-x-ray/t-SNE-EfficientNet-pneumonia.png)

![t-sne-TL-pneumonia](/assets/img/chest-x-ray/t-SNE-TL-pneumonia.png)

These t-SNE plots and confusion matrices show that the models are able to differentiate well between the normal and pneumonia classes but struggle with the viral pneumonia vs bacterial pneumonia classification. MobileNet performs better but the EfficientNet transfer learning model creates better separation of classes. 
Thus, even though MobileNet performs better in this case, the EfficientNet transfer learning model would generalize well on new unseen data. This is correlated in the confusion matrix where the transfer learning and MobileNet models perform the best.

Similarly, for the figure represents `T-SNE and Confusion matrices for the test set of the COVID dataset`.

![t-sne-all-covid](/assets/img/chest-x-ray/t-sne-all-covid.png)

- The above plots and confusion matrices also show that all models do a good job of separating classes to create distinct clusters but, the transfer learning model creates better clusters with separate smaller clusters. 
- These smaller clusters could indicate other factors of the disease, for example the severity and amount of lung damage caused by the disease. This performance of the transfer learning model can be confirmed by looking at the confusion matrix as well.

---

## Grad-CAM Visualizations

![grad-cam-pneumonia](/assets/img/chest-x-ray/grad-cam-pneumonia.png)

- The figure above shows the gradCAM visualization of the last layer of the convolutional network. Here, it can be seen that ResNet is learning completely different features as compared to the other models, which could be a reason of its poor performance. 
- In case of bacterial pneumonia, the network identifies affected area on the right side of the scan. On the other hand, incase of viral pneumonia, models look at both sides of the lungs.


Now, comparing the gradCAM visulization of the COVID dataset.

![grad-cam-COVID](/assets/img/chest-x-ray/grad-cam-COVID.png)

The figure above shows shows that MobileNet activates the entire image incase of COVID, this could be the reason for its low performance. In case of pneumonia, the Efficient- Net models identifies affected areas on the bottom of the lungs. On the other hand, in case of COVID, the models look at a bigger region of the lungs.

---

## Ablation Study

For the ablative study, the COVID dataset was chosen along with the EfficientNet B1 architecture trained from scratch. The learning rates chosen for the study are 0.001, 0.005, 0.01, 0.05, and 0.1.

![ablation-study](/assets/img/chest-x-ray/ablation-study.png)

- From the training and validation F1 score and loss plots given in the figure above. it is seen that a very high learning rate of 0.1 is highly unstable and prevents the model from reaching close to global minima. Similarly, learning rate of 0.05 also prevented the model from converging on the validation set even after 100 epochs. 
- The other three learning rates all converged on the validation set but, the learning rate of 0.001 was the most stable and reached the highest F1 score earliest. On the other hand, learning rate of 0.01 performed marginally better on the loss plot.

![ablation-study-graph](/assets/img/chest-x-ray/ablation-study-graph.png)

- From the figure above it can be seen that the best performing learning rate is 0.001 on the F1 score of the test set with 0.005, 0.01 close seconds and 0.05, 0.1 performing the worst. This matches the results of the validation set. Thus, a learning rate of 0.001 performs the best on the COVID dataset with transfer learning.

## Acknowledgement

`This writing has been written as per my and the collective understanding of our team followed by the learnings I kindled during my journey in this project. I hope you find it useful and easy to understand. I would appreciate any feedback or suggestions as well.`

<!-- <br/>

#### Other Team Members
[Rohan Chopra](https://github.com/rohanchopra), [Abhishek Handa](https://github.com/abhishekhandacse) and [Harmanpreet Kaur](https://github.com/harman8) -->

