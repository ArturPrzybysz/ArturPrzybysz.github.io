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

You can watch our teaser video: [here!](https://www.kaggle.com/danield2255/data-on-songs-from-billboard-19992019) 

## Dataset

The core part of our dataset comes from Wikipedia pages listing all the albums released from 1990-1999. 
There is one Wikipedia page for each year, with a title in the form “199X_in_music”, 
where all the albums released are being listed.  We combine it with a number of other sources, 
like other wikipedia pages we used to retrieve more detailed information on artists and each of the albums, 
which let us map the collaboration between artists. We use publicly available dataset such as 
[Billboard dataset from Kaggle](https://www.youtube.com/watch?v=OMDIm40BQ8s), 
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
Each node in the network has the following attributes:

* Spotify album features (danceability, energy, loudness, mode, speechiness, acousticness, instrumentalness, liveness, valence, tempo): The average value of every attribute is found for each album.
* Genres: All the genres associated with an artist.
* peak_rank: The highest rank an artist has achieved on the Billboard charts.
* weeks_on_chart: The accumulation of weeks on chart for all the artists' albums.
* last_week: The last week one of the artists' albums was on the charts.
* in_degree: The total number of in-references to the artist.
* out_degree: The total number of out-references the artist has.
* partition_id: The community the artist is placed in using the louvain algorithm [REFERENCE TODO].

A visualisation of the network can be seen below.`

![alt text for screen readers](/network_vis.png "Network visualisation").

For visualisation clarity, we decided to only display the names of the nodes
with at least 50 collaborations. This highlights the artists with the most collaborations.
The positions of the nodes have been calculated using the ForceAtlas2 algorithm [REFERENCE TODO].
We can see that the artists have been positioned in such a way, that they are close
to artists, that they collaborate with the most. This results in emerging of clusters.
We hypothesise, that it is highly influenced by artists' genre. A very good example of this is a group
of rappers, where we can see N.A.S., Snoop Dogg and The Notorious Bigg.

The network's statistics are following:

|            **Network statistic**            |                                   **Statistics' value**                                    |
|:-------------------------------------------:|:------------------------------------------------------------------------------------------:|
|              average in-degree              |                                            4.4                                             |
|             average out-degree              |                                            4.4                                             |
|         Average degree (in and out)         |                                            8.8                                             |
|   Nodes with highest degree of centrality   |                          Led Zeppelin, Mariah carey, Celine Dion                           |
|      Top connected artists (in-degree)      |                               The Beatles with 82 references                               |
|     Top connected artists (out-degree)      |                             Alanis Morissette with 108 albums                              |
| Pairs of artists that collaborated the most | Radiohead - Nigel Godrich (30 times), Opeth - Bloodbath (30), Radiohead - John Leckie (29) |

The in and out-degrees distributions are following:

![alt text for screen readers](/network_vis.png "Network visualisation")

![alt text for screen readers](/out_degree.png "Network visualisation")

The linear and log-log in-degree distribution are shown in the figures above.
Both these distributions follow the Power Law. We notice that there are many nodes with only a few links
(high frequency) and a few hubs (high degree) with large number of links.
The linear dependence in the log-log plot supports the idea that indeed, the graph follows the power distribution.

For this project, we have chosen to use an albums number of weeks on chart as a metric for success.
We want to examine the attributes of our nodes, to see if there is any correlation between these attributes and
the success of an artist. For this, we made a scatter plot of each node attributes against the weeks on chart and
computed the pearson correlation between these. See the scatter plot below.

<img alt="alt text for screen readers" height="500" src="/scatter1.png" width="500"/>

<img alt="alt text for screen readers" height="500" src="/scatter2.png" width="500"/>

From this, we found that there was a strong correlation between the number of weeks an artist had on the Billboard
charts and their number of collaborations.  This is interesting, as it points to the idea that the more popular you are
(i.e. the more weeks you have on the charts), the more collaborations you have! This is an interesting finding,
one that we would like to explore further. To do this we will look to determine what factors make two or more artists
collaborate together (see part TODO). This will give us more insight on what it takes to have many collaborations,
and thus have more success. 



Before we get to that though, we first want to explore our data further, to see if we find anything interesting.
We want to examine if there are other factors that are relevant to the success
of an artist, besides collaborations. For this we will dive into the lyrics of our artists, calculating TF-IDF scores,
making word clouds and performing sentiment
analysis on them, to see if there is something we can learn from this. Is there a correlation between sentiment of 
an artists' albums and their success? Does the genre of their music have an influence? Are there other factors that 
are important?

## Word Clouds

As mentioned earlier, we have used the Louvain algorithm [REF TODO] to partition the artists (our nodes) into
communities. We have 16 communities. In order to understand these communities better, i.e. what they represent,
we can look at what is important to them. For this, we will be using the lyrics from each artists' albums.
For each community, a select number of song lyrics of the artist's in that community are analyzed using the TFIDF
score [REF TODO]. We have then used this to make word clouds of the communities lyrics. A select number of these
can be seen below.

<img alt="alt text for screen readers" height="500" src="/wordcloud1.png" width="500"/>
<img alt="alt text for screen readers" height="500" src="/wordcloud2.png" width="500"/>
<img alt="alt text for screen readers" height="500" src="/wordcloud3.png" width="500"/>


To give an even better understanding, in the title of each word cloud, we have added the top 3 artists in that community
(the artists that have the most connections). These artists are meant to represent the communities in a way.
We see that in the word cloud where the top artists are Nas, The Notorious B.I.G. and a Tribe Called Quest, the biggest
words are typical rap lyrics that were found a lot in 90's rap music [INSERT REF TODO].
On the other side, the word cloud with the top artist's Weird Al Yankovic, The Red Hot Chili Peppers and The Foo Fighters
have words more in the genre of rock. The last word cloud, with the top artist's Paul McCartney, John Lennon
and Ringo Starr has more hippy lyrics, which probably doesn't surprise anyone, with its top artist's being 
members of the Beatles :-)

The purpose of the sentiment analysis part is to analyze the lyrics of different artists and albums in order
to determine if the sentiment score for each album in the network is influenced by specific features such as 
genre, year, trend in the number of collaborations etc. Ultimately, the analysis of this part investigates the 
interplay between the LabMT sentiment score and features such as number of collaborations or weeks in chart. 
In order to do so, we broke down our analysis into 3 levels: exploratory sentiment analysis of all the artists in 
the network, analysis of communities of artists and associated genres and analysis of the most successful artists.

<img alt="alt text for screen readers" height="500" src="/labmt_1.png" width="500"/>

For the purpose of this analysis, we found that LabMT is the most robust method to analyze our lyrics. From the 
histogram above, we notice that the values of sentiment score for LabMT method lie between 4.9 and 5.095. 
The histogram follows a Gaussian distribution, with most values centered around 5, but with the entire distribution 
being slightly skewed to the left. 

<img alt="alt text for screen readers" height="500" src="labmt_genres_top.png" width="500"/>

We found our that the analysis of the sentiment score per genre to be quite interesting, which is why we filtered 
our network for the top 30 most artists by sentiment score (artists represent the nodes in our network) and we 
extracted their associated genres. In the figure, we notice that some genres, such as girl group, ambient house and 
have a higher sentiment score than the others, such as hip-hop and punk. Considering that girl groups have met a 
wide success in the 90's, with famous bands such as Destiny's Child and Spicy Girls, it is no surprise that the 
genre is associated with very happy sentiments.

## Conclusion



## Sentiment analysis

### Lalala
Hasta manana
