---
title: "90's music data analysis"
date: 2021-12-08T15:04:05+01:00
draft: False
---

## Project introduction

In this project we are looking for an answer to the question: "What makes artists successful?". 
In order to find the answer we collect a wide range of data regarding artists' interactions, 
their artistic creations and popularity of their work.

We will first introduce you to the dataset we have created, then we will attempt to predict an artists' success directly. 
Finally, we get insight into the nature of collaborations between artists,
as we find that number of partnerships strongly correlates with artists' popularity.

## Dataset

The core part of our dataset comes from wikipedia pages listing all the albums released from 1990-1999. 
There is one wikipedia page for each year, with a title in the form “199X_in_music”, 
where all the albums released are being listed.  We combine it with a number of other sources, 
like other wikipedia pages we used to retrieve more detailed information on artists and each of the albums, 
which let us map the collaboration between artists. We use publicly available dataset such as 
[Billboard dataset from Kaggle](https://www.kaggle.com/danield2255/data-on-songs-from-billboard-19992019), 
APIs by Spotify or Genius to get insight into popularity, sound and lyric features.
From Spotify we retrieved song features such as danceability and energy.
From Billboard we retrieved data on which albums made it into the top charts and for how long.
From Genius we retrieved lyrics of the songs of the artists.
For a more detailed explanation of the dataset, please refer to explainer notebook available under TODO.


Once we combined all this data, we used our dataset for data analysis, looking to find what makes an artist successful.

## Data exploration
We begin our analysis by creating a network of artists, where the nodes are artists and the edges are collaborations among artists
through albums. To get the collaborations, we looked in every albums' wikipedia page and searched for references to other artists.
This means that the kinds of interactions that our network models are the following:
- collaborations in which musicians were co-creating another artists' album by playing instruments, singing or producing them,
- songwriters in the albums
- inspirations and covers
- former bands of the album authors.

Following this procedure we obtained a network which has 2763 nodes and 15108 edges. 
A visualisation of the network can be seen below.`

![alt text for screen readers](/network_vis.png "Text to show on mouseover").



### Lalala
Hasta manana
