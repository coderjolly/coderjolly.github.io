---
layout: post
title:  "Explaining Articles using LLMS"
date:   2024-01-10
title_include: true
categories: writing
image_url: ""
---

<style>body {text-align: justify}</style>

Natural Language Processing is the backbone of Language Models. They are used in a variety of tasks such as Machine Translation, Text Summarization, Question Answering, etc. This writing tries to understand how LLMs can be used to explain articles by using the pre-trained LLMs exposed on APIs such as OpenAI and GPT3.5 and how they can used for the task of article summarization, keyword generation, etc.

<figure>
<img src="/assets/img/llms/llm-llm-is.jpg" width=450 style="display: block; margin: 0 auto">
</figure>

## Architecture
The system uses a Flask backend which has been deployed as a backend service interacting with ``Celery`` workers and ``Redis`` for data caching. The architecture of the project is shown in the figure below which is a representation of the data pipeline and how different tasks like summarization, keyword generation can be handled by this pipeline.

![architecture](/assets/img/llms/pipeline-architecture.png)

The directory structure of the project is shown in the figure below which is the exact version as seen on Github.

<figure>
<img src="/assets/img/llms/directory-structure.png" width=450 height=650>
</figure>


Firstly, we use OpenAI to summarise the provided text because of its training model optimised by human feedback. Summarisation has the ability to not only shorten the length, but also improve the semantic details that fail to be noticed in lines of text. Secondly, we use Meaningcloud Text clustering API to cluster the summarised sentences based on their semantics and assign a descriptive label to each cluster. Instead of the basic document grouping mode, we choose the topic modelling mode implemented with the K-means algorithm. This approach helps to discover hidden themes in sentences by providing more descriptive labels than classical clustering algorithms. With the descriptive labels of each cluster, we again used OpenAI to extract the keywords from the summarised transcriptions. Instead of RAKE, Spacy, and TextRank, we chose OpenAI as it suits the context of the work. For example, only OpenAI supports extraction of both key- word and keyphrases. The industry explorations reveal that the keywords extracted by OpenAI were more meaningful and closer to reflect the gist of text provided. For layers with optional image toggles, we fetched the images based on each keyword/keyphrase using Google Image Search.


<h1 style="text-align:left;" >Under Construction. Uh oh!</h1>
<section class="lost-container">
  <!-- <h1 style="text-align:left;" >Uh oh!</h1> -->
  <div style="text-align:left;" class="link">
    <img class="selfie" alt="{{ site.title }}" src="{{ site.url }}/assets/img/error.gif" />
      <br /> <br /> <br />
    <a href="/">Take me home!</a>
  </div>
</section>
