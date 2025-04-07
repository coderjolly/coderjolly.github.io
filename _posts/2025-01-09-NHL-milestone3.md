---
layout: post
title:  "NHL Milestone 3"
date:   2025-01-09
title_include: true
categories: writing
image_url: ""
---

### Milestone 3 Objective
This milestone did not require any report or blog post. Instead, we were required to simply provide the github repository of our source code.  
Here, we provide a link to a video in which we demonstrate the execution of our docker containers.  

The objective is to create a Streamlit client app and a Flask server app. Each of these apps is deployed in a separate docker container.  
The Streamlit client app lets the user select a model to predict the outcome of a game, based on the game's shot-on-goal data. The user can select any NHL game (past or live!) by sending the NHL game ID to the server.  
The Flask server is responsible for receiving the game ID, retrieving the game data from the database, and sending the data to the model. The server can pull different models we trained in the previous milestone, which are stored in the Weights and Biases cloud.  

### Milestone 3 Video
<!-- The video starts by starting both containers with the `docker-compose up` command.  
Then, the client app is demonstrated into the browser. The user can select a model and the game ID.  -->
The user can select a model and the game ID. The game ID selected was actually live during the recording of the video ([April 5th, 2025, Montreal Canadian vs. Philadephia Flyers](https://www.nhl.com/gamecenter/mtl-vs-phi/2025/04/05/2024021217)).  
We can see that the first select model predicts "2.7" goals for the Flyers, and "3.1" goals for the Canadians, while the score was 2-3 when recording the video (there were 10 minutes left in the last period).