---
layout: full-width
title: Projects
weight: 2
---
<style>body {text-align: justify}</style>


**Explaining Articles using LLMs** [**[<font color='blue'>Writing</font>]**](articles/24/explaining-news-using-llms){:target="_blank"}{:target="_blank"}
<br/>

<div style="display: flex; flex-wrap: wrap; align-items: center;">
    <div style="flex: 1; margin-right: 10px;">
        <p style="font-family: 'cascadia'; font-size: 1.02rem; border-radius: 3px; color: #a00000; font-weight: 500;">
            Natural Language Processing is the backbone of Language models. They are used in a variety of tasks such as Machine Translation, Text Summarization, Question Answering, etc. This writing tries to understand how LLMs can be used to explain news articles by using the pre-trained LLMs exposed on APIs such as OpenAI and GPT3.5 and how they can used for the task of article summarization, keyword generation, etc.</p>
        </div>
        <div style="flex: 1; margin-left: -10px; margin-top: 10px;">
            <img src="/assets/img/llms/pipeline-architecture.png" alt="Image" style="width: 100%; max-width: 475px; height: 275px;">
        </div>
</div>

**Processing Image Advertisements for Contextual Analysis** [**[<font color='blue'>Writing</font>]**](articles/23/processing-ads){:target="_blank"} [**[<font color='blue'>Github</font>]**](https://github.com/coderjolly/processing-advertisements){:target="_blank"}
<br/>

<div style="display: flex; flex-wrap: wrap; align-items: center;">
    <div style="flex: 1; margin-right: 10px;">
        <p style="font-family: 'cascadia'; font-size: 1.02rem; border-radius: 3px; color: #a00000; font-weight: 500;">
            Image based advertisements are still one of the best ways to promote products but it is difficult to personalize the content for the audience and covey the context. This study tries to compare three backbone deep learning architectures namely, ResNet 50, MobileNetv3 Large and EfficientNet B3 on an image advertisement dataset to classify the underlying contexts or sentiments understood by the consumers. Transfer learning is applied to mitigate the small dataset problem.</p>
        </div>
        <div style="flex: 1; margin-left: -10px; margin-top: 10px;">
            <img src="/assets/img/image-advertisements/pre-processing.png" alt="Image" style="width: 100%; max-width: 350px; height: 250px;">
        </div>
</div>

**Steamgestion - A Data Ingestion Pipeline** [**[<font color='blue'>Writing</font>]**](articles/22/steamgestion-data-pipeline){:target="_blank"} [**[<font color='blue'>Github</font>]**](https://github.com/coderjolly/data-ingestion-pipeline){:target="_blank"}
<br/>

<div style="display: flex; flex-wrap: wrap; align-items: center;">
    <div style="flex: 1; margin-right: 10px;">
        <p style="font-family: 'cascadia'; font-size: 1.02rem; border-radius: 3px; color: #a00000; font-weight: 500;">
        Gaming industry is one of the most prominent industries in the market. To determine the popularity of a game, reviews are of paramount importance. This project aims to analyse Steam reviews dataset using a Distributed System Design which is a Flask asynchronous backend which incorporates an Elasticsearch engine deployed in a Docker-Kubernetes environment where data ingestion queues are handled by RabbitMQ, processes are handled by Celery & data is cached in Redis.</p>
    </div>
    <div style="flex: 1; margin-left: -10px; margin-top: 10px;">
        <img src="/assets/img/steamgestion/architecture.png" alt="Image" style="width: 100%; max-width: 350px; height: 250px;">
    </div>
</div>


**Credit Risk Modelling** [**[<font color='blue'>Writing</font>]**](articles/23/credit-risk-modelling){:target="_blank"} [**[<font color='blue'>Github</font>]**](https://github.com/coderjolly/credit-risk-modelling){:target="_blank"}
<br/>

<div style="display: flex; flex-wrap: wrap; align-items: center;">
    <div style="flex: 1; margin-right: 10px;">
        <p style="font-family: 'cascadia'; font-size: 1.02rem; border-radius: 3px; color: #a00000; font-weight: 500;">
        <!-- <code class="language-plaintext highlighter-rouge"> -->
        Credit risk is the risk of loss that may occur from the failure of any party to abide by the terms and conditions of any financial contract, principally, the failure to make required payments on loans. This project aims to predict the credit risk of a customer. The data is cleaned, preprocessed, visualised and then used to various machine learning algorithms by oversampling and undersampling the dataset.</p>
        </div>
        <div style="flex: 1; margin-left: -10px; margin-top: 10px;">
            <img src="/assets/img/credit-card-risk-modelling/imbalanced-scenario.png" alt="Image" style="width: 100%; max-width: 475px; height: 250px;">
        </div>
</div>


**Lung Disease Classification using Chest X-rays** [**[<font color='blue'>Writing</font>]**](articles/22/chest-x-ray){:target="_blank"} [**[<font color='blue'>Github</font>]**](https://github.com/coderjolly/Chest-X-Ray-Classification){:target="_blank"}
<br/>

<div style="display: flex; flex-wrap: wrap; align-items: center;">
    <div style="flex: 1; margin-right: 10px;">
        <p style="font-family: 'cascadia'; font-size: 1.02rem; border-radius: 3px; color: #a00000; font-weight: 500;">
        Chest X-rays scans are among the most accessible ways to diagnose lung diseases. This study tries to compare the detection of lung diseases using xray scans from three different datasets using three different neural network architectures using Pytorch and perform an ablation study by changing learning rates. The dimensional understanding is visualized using t-SNE and the ditection of thorax deseases in x-ray scans is visualized using Grad-CAM.</p>
        </div>
        <div style="flex: 1; margin-left: -10px; margin-top: 10px;">
            <img src="/assets/img/chest-x-ray/histogram-equilization.png" alt="Image" style="width: 100%; max-width: 475px; height: 275px;">
        </div>
</div>

**Depression Data Collection Portal** [**[<font color='blue'>Writing</font>]**](articles/23/find-help){:target="_blank"} [**[<font color='blue'>Github</font>]**](https://github.com/coderjolly/find-help){:target="_blank"}
<br/>

<div style="display: flex; flex-wrap: wrap; align-items: center;">
    <div style="flex: 1; margin-right: 10px;">
        <p style="font-family: 'cascadia'; font-size: 1.02rem; border-radius: 3px; color: #a00000; font-weight: 500;">
        A backend application based on Java Spring Boot that caters to the need of collecting data for patients with depression. Patients are able to register themselves, perform self assessment in order to get help from a counsellor or doctor. This self-assessment data will be communicated to a counsellor or doctor and then appropriate action will be taken accordingly.
        </p>
        </div>
        <div style="flex: 1; margin-left: -10px; margin-top: 10px;">
            <img src="/assets/img/find-help/home-page.png" alt="Image" style="width: 100%; max-width: 475px; height: 275px;">
        </div>
</div>


**News Recommendation System** [**[<font color='blue'>Github</font>]**](https://github.com/coderjolly/news-recommender){:target="_blank"}
<br/>

<div style="display: flex; flex-wrap: wrap; align-items: center;">
    <div style="flex: 1; margin-right: 10px;">
        <p style="font-family: 'cascadia'; font-size: 1.02rem; border-radius: 3px; color: #a00000; font-weight: 500;">
        Nowadays, online news is accessible to millions with news articles from multiple sources. In order to help users find the right and relevant content, news recommender systems suggest articles that might be of interest for the news readers. So, using beautiful-soup to scrap news articles, their categories and descriptions a textual corpus is created. It then uses word embedding techniques such tf-idf, word2vec for content based news recommender models and LightRF, LightFM to explore collaborative filtering based recommender models.</p>
        </div>
        <div style="flex: 1; margin-left: -10px; margin-top: 10px;">
            <img src="/assets/img/news-recommender/web-scrapping.png" alt="Image" style="width: 100%; max-width: 450px; height: 230px;">
        </div>
</div>


**Football Player Market Value Prediction** [**[<font color='blue'>Github</font>]**](https://github.com/coderjolly/football-player-prediction){:target="_blank"}
<br/>

``You must have seen "Moneyball", where Peter Brand explains Billy Beane that "Its about getting things down to one number using stats the way we read them (players), we find value in player nobody else can see." So, to predict this Market Price of players, data from a csv is ingested and then applied to machine learning algorithms.``
<!-- for comparing their R^2 values and an EDA is performed to understand the data in negotiating players for transfers -->


**Bird Call Audio Classification** [**[<font color='blue'>Github</font>]**](https://github.com/coderjolly/bird-call){:target="_blank"}
<br/>

``With proper sound detection and classification, researchers can understand what birdcall signal the birds use, in order to communicate with each other or to warn others about the impending dangers in the vicinity. So, understanding the bird species via sound can able to detect theses dangers early. Mel Spectrograms of these bird audios are used as features to feed them to a CNN model in order to classify bird species.``

**DonorFu** [**[<font color='blue'>Devpost</font>]**](https://devpost.com/software/donorfu){:target="_blank"}
<br/>

``We find many groups on facebook catering to blood requests. Some groups are highly active and thus cluttered with requests, others dormant & requests are unanswered. DonorFu, a facebook messenger bot leverages access to groups approved by admins to match posts with potential donors to manage these groups which won $17,500 at FB Developer Community Challenge.``


<!-- **Customer Churn Prediction** [**[<font color='blue'>Github</font>]**](https://github.com/coderjolly/customer-churn-prediction){:target="_blank"}
<br/>

``Customers play an integral role in the success of any business. So, it is important to understand the customer behaviour and predict their churn. This project aims to predict the churn of customers using a dataset from Kaggle. The data is visualised and preprocessed and then fed to classical machine learning algortihms for classification.`` -->

<!-- <table>
<tr>
<th><b>Projects</b></th>
<th><b>Description</b></th>
</tr>
<tr>
<td>
<b>Utilization Analysis</b>
</td>
<td>
<font color='maroon'>This provides a small glimpse of the SERC's resource data demonstrating how data was ingested and extracted to produce relevant results for data analysis between actual resource utilization and simulated resource utilization.</font>
</td>
</tr>

<tr>
<td>
<b>Sociogram</b>
</td>
<td>
<font color='maroon'>Nowadays, image posting is considered a pivotal social media interaction for sharing posts. SocioGram is an application that allows users to upload various pictures and share it on their profile. Other users can leave a comment or a like on the pictures accordingly, built using Ruby on Rails and Bootstrap.</font>
</td>
</tr>

</tr>
</table> -->