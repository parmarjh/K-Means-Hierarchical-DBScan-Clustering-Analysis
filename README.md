# K-Means-Hierarchical-DBScan-Clustering-Analysis #
Hyperparameter Tuning of K-Means using Elbow Method, Eps values based on MinPoints for DBScan and Hierarchical Clustering based on various values of 'k' is done to form different clusters, on which an analysis is done for semantic coherence. 

## Amazon Fine Food Review Dataset ##

**Data Source**: https://www.kaggle.com/snap/amazon-fine-food-reviews

The Amazon Fine Food Reviews dataset consists of **reviews of fine foods from Amazon**. <br/>
Number of reviews                   : **568,454**  <br/>
Number of users                     : 256,059  <br/>
Number of products                  : 74,258  <br/>
Timespan: Oct 1999                  : Oct 2012  <br/>
Number of Attributes/Columns in data: 10 <br/>

### Attribute Information ###
1. Id <br/>
2. ProductId - unique identifier for the product <br/>
3. UserId - unqiue identifier for the user <br/>
4. ProfileName <br/>
5. HelpfulnessNumerator - number of users who found the review helpful <br/>
6. HelpfulnessDenominator - number of users who indicated whether they found the review helpful or not <br/>
7. Score - rating between 1 and 5 <br/>
8. Time - timestamp for the review <br/>
9. Summary - brief summary of the review <br/>
10. Text - text of the review <br/>

## Objective ##

The code below would **clean the review text from html tags and punctuations and write it as a new column in the database and write it to disk**. This is further taken up in Part 2 to find accuracy of 10-fold cross validation KNN on vectorized input data, for each of the 4 featurizations, namely BoW, tf-IDF, W2V, tf-IDF weighted W2V.

## Significant Points ##

1. **Duplication of reviews** are found with same userid and timestamp (Cleaned).
2. Found discrepancy issues with HelpfulnessDenominator (Cleaned).
3. final.sqlite db is **to be used for further processing** such as Text to Vector operations.
4. The preprocessing step is one time effort but the training & visualization steps require multiple runs. Hence, it is prudent to make reprocessing step independant, to avoid multiple runs.

# K-Means-Hierarchical-DBScan-Clustering-Analysis (Part II) #

## Data Source: ##

**The preprocessing step has produced final.sqlite file after doing the data preparation & cleaning.** The review text is now devoid of punctuations, HTML markups and stop words.

## Objective: ##

To find meaningful clusters using **unsupervised clustering algorithms like K-Means, Hierarchical & DBScan** on the review dataset. The **polarity of the review is removed from the input dataset**, so that the clustering would happen just on the review text given.

4 standard featurizations are used, namely **BoW, tf-idf, W2V and tf-idf weighted W2V featurizations**. Cross validaton or test metrics in supervised algorithm cannot be used as there is no test data. Instead, **random samples from clusters formed are analyzed manually and a conclusion should be arrived at**.

## At a glance: ##

The **elbow method is used to find the right # of clusters of K-Means. The minPoints for DBScan is set as double the number of dimension of W2V vectors**, as a rule of thumb. The **Eps value is calculated using KNN distance plots**. The point at which the slope of the plot is higher than a set threshold is taken as Eps value.

The hierarchical clustering algorithm is run with different ‘k’ values & DBScan also is executed with different Eps values. so that the impact of change in hyperparameters can be well understood.

## Custom Defined Functions ##

**3 user defined functions are written to**

**a) Compute Mean Neighbourhood Distance & Distance Plot**

**b) Elbow Method to find K**

**c) Analyze the Clusters function.**

## K-Means & Hierarchical Clustering on BoW ##

BoW will result in a **sparse matrix with huge number of features** as it creates a feature for each unique word in the review.

For Binary BoW feature representation, CountVectorizer is declared as float, as the values can take non-integer values on further processing.

<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/8.1.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/8.2.PNG">
</p>
<p align="center">
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/8.3.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/8.4.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/8.5.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/8.6.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/8.7.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/8.8.PNG">
</p>

## K-Means & Hierarchical Clustering on tf-IDF ##

**Sparse matrix generated from tf-IDF** is fed in to GridSearch GBDT Cross Validator & RF Cross Validator to find the optimal depth value. Performance metrics of optimal GBDT with tf-idf featurization is found.

<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/9.1.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/9.2.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/9.3.PNG">
</p>
<p align="center">
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/9.4.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/9.5.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/9.6.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/9.7.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/9.8.PNG">
</p>

## K-Means, Hierarchical Clustering & DBScan on Word2Vec ##

**Dense matrix generated from Word2Vec** is fed in to GridSearch GBDT Cross Validator & RF Cross Validator to find the optimal depth value. Performance metrics of GBDT and RF with W2V featurization is found.

<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.1.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.2.PNG">
</p>
<p align="center">
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.3.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.4.PNG">
</p>
<p align="center">
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.5.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.6.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.7.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.8.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.9.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.10.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.11.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.12.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.13.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.14.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.15.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.16.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.17.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.18.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.19.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/10.20.PNG">
</p>

## K-Means, Hierarchical Clustering & DBScan on TF-ID Weighted W2V ##

<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.1.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.2.PNG">
</p>
<p align="center">
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.3.PNG">
</p>
<p align="center">
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.4.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.5.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.6.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.7.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.8.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.9.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.10.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.11.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.12.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.13.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.14.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.15.PNG">
</p>
<p>
    <img src="https://github.com/AdroitAnandAI/K-Means-Hierarchical-DBScan-Clustering-Analysis/blob/master/images/11.16.PNG">
</p>

## Observations ##

1. **All the clusters are formed based on word (or contextual similarities) and NOT on +ve or -ve review rating as they are not given ‘y’ values as input, while clustering**.

2. The analysis of clusters formed using 4 featurizations are done.

    **1. BoW**
    
        K-Means:
        
        Cluster 0: most reviews about taste of food derived from flavour.
        Cluster 1: reviews focussed on ‘work’ environment products. Eg: office, work, colleagues, receptionist etc are repeated.
        Cluster 2: groups reviews related to food. The repeated words are food, sugar, flours, oil etc.
        
        Hierarchical:
        
        The clustering is not meaningful as all points except 1, is grouped into 1 single cluster.
        
    **2. tf-idf**
    
        K-Means:
        
        Cluster 0: customers are in dilemma. Whether the effectiveness is +ve or -ve or just placebo.
        Cluster 1: talks about illness and effectiveness of medicines. Many medical terminologies.
        Cluster 2: all reviews are about sound and equipments related to sound. Eg: mic, icicle, jack etc.
        Cluster 3: groups reviews related to food. The repeated words are food, sugar, flours, oil etc.
        
        Hierarchical:
        
        The clustering is not meaningful as all points except 1, is grouped into 1 single cluster.
        
    **3. Word2Vec:**
    
        K-Means:
        
        From the cluster groups, it can be seen that the **reviews obtained from kmeans clustering are more distributed**.
        
        Cluster 0: Reviews are going in-depth about using the purchased product for cooking. Eg: noodies, oil, chicken, ice cream, etc.
        Cluster 1: There are some negative words (reviews) repeated, in this group. Some breakfast products are clubbed in this group.                  Eg: cornflakes, peanut butter etc.
        Cluster 2: This group is all about drinks. Eg: coffee, chai, latte, cups, drink, chocolate etc are repeated.
        Cluster 3: Extremely positive reviews. Most of the reviews are about products which are rarely available in the market, but only                in Amazon. Logically, as customers were able to find such ‘hard-gets’, they are extremely happy.
        Cluster 4: This group focus on delivery and damage caused for the shipment. 
        Cluster 5: Most of the reviews are about bakery food items. Product reviews are about chocolate syrup, scones, shortbread, ice                  cream, carbonated drinks and fruit juice etc.
        Cluster 6: Groups products available in amazon, vis-a-vis offline stores.
        Cluster 7: This group is all about tea and tea products.
        Cluster 8: This group is all about pets, mostly dog and cats.
        Cluster 9: Group focus on energy drinks and health drinks.
        Cluster 10: Groups reviews about Bread and associated combinations.
        Cluster 11: Very personal opinion about the products are shared.
        Cluster 12: This group is all about dog food and cat food.
        Cluster 13: Groups reviews about healthy related products and meal replacements. Eg: protein bars, energy bars, pirate booty,
                healthy cereal etc.
        Clusters 14: Snacks & toffees are grouped. Eg: rice chips, toffee, pepper, berger, chocolate etc.
        
        Hierarchical:
        
        The first 2 clusters formed when K=2 & K=5 are similar.
        
        Cluster 0: Groups reviews about snacks and sauces.
        Cluster 1: Groups cuisines of different cultures.
        Cluster 2: Groups tea and coffee reviews.
        Cluster 3: Nothing found in common.
        Clsuter 4: Groups dog and cat foods.
        
        DBSCAN:
        
        The Eps value is found out using Min Points value. 2 Clusters are formed while using the computed Eps value. One cluster has id         of -1, which means they are identified as noise. When Eps value is reduced all the points are identified as noise, whereas, when         the Eps value is increased, then number of noise points drastically reduced.
        
    **4. tf-idf W2V:**
    
        K-Means:
        
        The 15 clusters formed via tf-idf weighted W2V vectors have similar grouping pattern compared to W2V vectors. The cluster   
        separation may be slightly more meaningful than using W2V alone, but they are not significantly better.
        
        Hierarchical:
        
        The 5 clusters formed are similar to the groups obtained from W2V method, but they are more meaningfully separated. For                 instance, Cluster 3 talks only about dogs and dog foods, whil Cluster 4 contains reviews about different variants of tea, such           as black tea, green tea etc.
        
        DBSCAN:
        
        The DBSCAN results shows similar results as with W2V vector. When Eps value is reduced all the points are identified as noise,           whereas, when the Eps value is increased, noise points are reduced.
        
 3. From the above analysis, it can deduced that **K-Means algorithm on TF-IDWeighted W2V orWord2Vec is the clustering algorithm of choice**.
