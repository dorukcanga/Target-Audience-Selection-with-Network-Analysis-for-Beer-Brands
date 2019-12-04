# Target Audience Selection with Network Analysis for Beer Brands Project
Final project of DA516 Network Analysis Course of MSc in Data Analytics in Sabancı University.

Methodology explained in [this paper](https://web.b.ebscohost.com/abstract?direct=true&profile=ehost&scope=site&authtype=crawler&jrnl=02767783&AN=119473687&h=QV6vJcqFVsifjSSvTnweFKB3GJwDCo%2fvykJ5raAdqEirFCvRHSpAQIBeDORnM2zmVXxQL%2beYpovJPzd4b50idw%3d%3d&crl=c&resultNs=AdminWebAuth&resultLocal=ErrCrlNotAuth&crlhashurl=login.aspx%3fdirect%3dtrue%26profile%3dehost%26scope%3dsite%26authtype%3dcrawler%26jrnl%3d02767783%26AN%3d119473687) 
named "Large-Scale Network Analysis for Online Social Brand Advertising 
and written by Kunpeng Zhang, Siddhartha Bhattacharyya, Sudha Ram is implemented to beer brands.

## Project Purpose

The purpose of the project is determination of target audience for advertising for beer brands using network analysis.

## Dataset

Dataset contains several information on beer brands, their ratings given by various users and User reviews.
User reviews are excluded from the scope of this study. 
There are 1.586.614 records entered by 33.388 users for 66.055 beers in dataset.

**Columns of the dataset are as follow:**
* Beer Name
* Beer ID
* Brewer ID
* Alcohol by Volume
* Beer Style
* User Name
* Appearance Rating
* Aroma Rating
* Palate Rating
* Review Taste
* Review Overall
* Review Date
* Review Content

## Project Outline

### Data Preprocessing

* Removing Spams

Removing the reviewers which reviewed beers above a threshold (spam).

* Removing Empty Line

Removing lines which ReviewProfileName is empty.

* Removing Older Reviews

Removing the reviews before 2002 due to unbalanced ratings and limited number.

* Removing Beers with Few Reviews

Removing the beerIds which the total number of reviews is less than a threshold.

* Removing Reviewers with Few Reviews

Removing the reviewers which has reviews less than a threshold.

### Network Generation

* Creating Bipartite Graph

Bipartite Graph consisting of BeerIds and User names.

* Creating Undirected Weighted Network

Undirected Weighted Network is projected from bipartite graph.
weights of the edges of the network determined by number of common users between nodes.
Edges with weight less than 30 (Weak connections) are removed from network.

* 2 Step Weight Normalization

In first step, weights are normalized by 2 nodes of edges and secondly all weights are normalized globally by dividing them to maximum weight of the network.
Normalization is done to better compare edges, in other words connection strength.

* Network Analysis

Following analysis are made: Average Degree, Degree Distribution, Average Clustering Coefficient, Average Shortest Path Length, Degree Centrality

* Community Detection

Louvain method is implemented to detect community structure of the network that maximize modularity.
Network is splitted to 4 communities.

* Finding Similar Beers to Focal Beers

Node2Vec algorithm is implemented and vectors with 64 dimensions for all nodes are calculated.
50 most similar beers which are in the same community with focal beer are detected wşth cosine similarity values of the vectors.

* Target User Selection

From most similar 50 beers to the focal beer, top n users who have given highest rating (and at least k rating, for example 4.5/5 rating) 
of all 50 selected beers as similar are selected as target audience.

* Model Evaluation

Average of ratings given to focal beer by users who have already given rating to focal beer and who are selected as target audience 
is compared average of ratings given to focal beer by users who are not selected as target audience.

