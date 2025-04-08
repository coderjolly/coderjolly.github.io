---
layout: post
title:  "NHL Highlights"
date:   2025-01-10
title_include: true
categories: writing
image_url: ""
---

<style>body {text-align: justify}</style>

[[``MileStone1``]({{ site.url }}/articles/24/NHL-milestone1){:target="_blank"},
[``MileStone2``]({{ site.url }}/articles/24/NHL-milestone2){:target="_blank"},
[``MileStone3``]({{ site.url }}/articles/25/NHL-milestone3){:target="_blank"}]


## 🎥 Demo Video

The client app is demonstrated into the browser. The user adds a game ID. The game ID selected was actually live during the recording of the video ([April 5th, 2025, Montreal Canadiens vs. Philadephia Flyers](https://www.nhl.com/gamecenter/mtl-vs-phi/2025/04/05/2024021217)).  
We can see that the first select model predicts "2.7" goals for the Flyers, and "3.1" goals for the Canadians, while the score was 2-3 when recording the video (there were 10 minutes left in the last period).  

<iframe src="https://drive.google.com/file/d/11Z9Dw3AwkNmQ5LknK-qlmpshpDs4FS_k/preview" 
        width="700" height="394" 
        allow="autoplay">
</iframe>


<!-- ## Table of Contents
- [🎥 Demo Video](#-demo-video)
- [Table of Contents](#table-of-contents)
- [1. Data Acquisition and Visualisation](#1-data-acquisition-and-visualisation)
  - [1.1 Data Acquisition](#11-data-acquisition)
  - [1.2 Simple Visualizations](#12-simple-visualizations)
  - [Shot types](#shot-types)
    - [Goal rate vs distance](#goal-rate-vs-distance)
    - [Shot vs distance and shot-type](#shot-vs-distance-and-shot-type)
  - [1.3 Advanced Visualisations](#13-advanced-visualisations)
- [2. Feature Engineering and Model Training](#2-feature-engineering-and-model-training)
  - [2.1 Histogram of shot counts binned by shot distance and shot angle](#21-histogram-of-shot-counts-binned-by-shot-distance-and-shot-angle)
  - [2.2 Plotting Goal Rate (Goal/(No Goals + Goals)) binned by distance and shot angle](#22-plotting-goal-rate-goalno-goals--goals-binned-by-distance-and-shot-angle)
  - [2.3 Plotting Histograms of empty and non-empty goals](#23-plotting-histograms-of-empty-and-non-empty-goals) -->

## 1. Data Acquisition and Visualisation
**NOTE** : A more detailed version of this section is documented in the this [link]({{ site.url }}/articles/24/NHL-milestone1).

### 1.1 Data Acquisition

In this section, we first download the play-by-play events for each game using the publicly available NHL API:

[https://api-web.nhle.com/v1/gamecenter/{GAME_ID}/play-by-play](https://api-web.nhle.com/v1/gamecenter/{GAME_ID}/play-by-play)

To fetch the play-by-play events of a game of your choice, it is recommended to follow the following format:

Figuring out Game IDs for each season:

Since we download play-by-play events from each game (Regular and Playoffs) from seasons 2016-2017 to 2023-2024, we break-down the logic behind the naming of GAME_ID as mentioned in the following link :

[NHL API Game IDs Documentation](https://gitlab.com/dword4/nhlapi/-/blob/master/stats-api.md#game-ids)

In brief, suppose we take GAME_ID ``` 2019020901 ``` and GAME_ID ``` 2021030217 ``` , the breakdown from left to right would be as follows:

``` 2019020901 ```
- '2019' for the season 2019-2020.
- '02' for regular season.
- '0901' for game number 901 in the regular season.

``` 2021030217 ```
- '2021' for the season 2021-2022.
- '03' for the playoff season.
- '0217' -> For playoff games, the 2nd digit of the specific number gives the round of the playoffs, the 3rd digit specifies the matchup, and the 4th digit specifies the game (out of 7). (In this example: 7th game of match #1 in playoff round 2.)

In our project, we ping each game and cache the play-by-play events for ALL NHL games from seasons 2016-2017 to 2023-2024 (including regular and playoffs games!). For more explanations, we have a [detailed webpage]({{ site.url }}/articles/24/NHL-milestone1){:target="_blank"} dedicated to this section.

### 1.2 Simple Visualizations

All the following plots were obtained using the cumulative play-by-play data from all seasons and games mentioned in the previous section.

### Shot types

**NOTE** for detailed explanations for this section follow this [link]({{ site.url }}/articles/24/NHL-milestone1).

Important note: for this analysis, we have decided to drop shot types that have been used less than 0.1%, because they don't represent meaningful information, especially when compared to other shot types.
The shot types dropped were "between-legs" and "cradle", with 0.06% and 0.005% usage, respectively.

<img src="/assets/img/NHL/simple_viz_shot_types.png" alt="2023-2044 Season Shot Types Bar plot">

#### Goal rate vs distance 

<img src="/assets/img/NHL/simple_viz_goal_conversion.png" alt="Goal Conversion Rate for Seasons 2018, 2019 and 2020">

#### Shot vs distance and shot-type

<img src="/assets/img/NHL/simple_viz_goal_conversion_vs_dist1.png" alt="Goal Conversion Rate for Season 2023, per shot type">
<img src="/assets/img/NHL/simple_viz_goal_conversion_vs_dist2.png" alt="Goal Conversion Rate for Season 2023, per shot type">

### 1.3 Advanced Visualisations

For the advanced visualisations, we have decided to include missed shots in our calculations to get a more complete picture of offensive performance.

<!-- Dropdown Menu for Selecting Year -->
<div style="display: flex; align-items: center;">
  <h4 style="margin-right: 10px;">Select the season to display</h4>
  <select id="yearDropdown">
    <option value="2016">2016-2017</option>
    <option value="2017">2017-2018</option>
    <option value="2018">2018-2019</option>
    <option value="2019">2019-2020</option>
    <option value="2020">2020-2021</option>
  </select>
</div>

<!-- Hide the figures -->
<div id="plotly_2016" class="plotly-figure" style="display:none;">
  {% include plotly_2016.html %}
</div>
<div id="plotly_2017" class="plotly-figure" style="display:none;">
  {% include plotly_2017.html %}
</div>
<div id="plotly_2018" class="plotly-figure" style="display:none;">
  {% include plotly_2018.html %}
</div>
<div id="plotly_2019" class="plotly-figure" style="display:none;">
  {% include plotly_2019.html %}
</div>
<div id="plotly_2020" class="plotly-figure" style="display:none;">
  {% include plotly_2020.html %}
</div>

<!-- JavaScript for Toggling Figures -->
<script>
  document.getElementById('yearDropdown').addEventListener('change', function() {
    // get the selected year from the dropdown
    var selectedYear = this.value;

    // hide all figures
    var figures = document.querySelectorAll('.plotly-figure');
    figures.forEach(function(figure) {
      figure.style.display = 'none';
    });

    // show the figure that matches the selected year
    document.getElementById('plotly_' + selectedYear).style.display = 'block';
  });

  // show the first figure by default
  document.getElementById('plotly_2016').style.display = 'block';
</script>

## 2. Feature Engineering and Model Training

### 2.1 Histogram of shot counts binned by shot distance and shot angle

**NOTE**: The 'Non-Goals' are shots classified as 'shot-on-goal' and 'missed-shots' in our data for seasons from 2016-2017 upto 2019-2020(4 seasons). Additionally, shot angles are higher for shots that are taken head-on. For example, a shot angle of 90 degrees means it is directed along the same line as taking a shot from the centre of the pitch towards goal.

Plotting histogram of shot counts binned by shot distance:

<img src="/assets/img/NHL/Feature1_binshots_dist.png" alt="Goals by distance">
<img src="/assets/img/NHL/Feature1_binshotNg_distance.png" alt="Non-goals by distance">

A more detailed version of this section is documented in the this [link]({{ site.url }}{{ site.baseurl }}/2024/11/13/milestone-2)

Plotting histogram of shot counts binned by shot angle:

<img src="/assets/img/NHL/Feature1_binshotG_angle.png" alt="Goals by angle">
<img src="/assets/img/NHL/Feature1_binshotsNg_angle.png" alt="Non-goals by angle">

### 2.2 Plotting Goal Rate (Goal/(No Goals + Goals)) binned by distance and shot angle

Goal rate by shot distance:

<img src="/assets/img/NHL/Feature1_bingoals_distance.png" alt="Goal rate by distance">

Goal rate by shot angle:

<img src="/assets/img/NHL/Feature1_bingoals_angle.png" alt="Goal rate by angle">

### 2.3 Plotting Histograms of empty and non-empty goals

<img src="/assets/img/NHL/Feature1_emptygoals_dist.png" alt="Empty goals by distance">

<img src="/assets/img/NHL/Feature1_nonempty_distance.png" alt="Non Empty goals by distance">


## 3. Deployment and Dependeancy Management

<img src="/assets/img/NHL/soft-eng-meme.png" width=450 style="display: block; margin: 0 auto">

To operationalize the expected goals (xG) models for NHL game predictions, we designed a lightweight, modular deployment pipeline using Flask, Docker, and Docker Compose.

🔌 Flask API for Model Serving
I built a RESTful Flask application that exposes endpoints to:

- /predict: Score new shot events and return xG predictions.
- /logs: View runtime activity.
- /download_registry_model: Swap models live from the Weights & Biases model registry without restarting the app.

📦 Containerized Deployment with Docker

<img src="/assets/img/NHL/docker-meme.png" width=450 style="display: block; margin: 0 auto">

Managing Python dependencies, version mismatches, and environment drift is a common challenge in ML projects. To solve this, I containerized the entire application using Docker, ensuring:

- Reproducibility across systems and collaborators.
- Seamless version control of dependencies via requirements.txt.
- Lightweight builds without bundling model weights inside the container (thanks to dynamic hot-swapping).

