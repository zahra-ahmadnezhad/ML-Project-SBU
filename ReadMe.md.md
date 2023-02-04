## Incorporating K-means, Hierarchical Clustering  and PCA in Customer Segmentation 


#### DATA

The data consists of 8950 observations (rows) related to the credit card holders as registered users of a European credit card company, and 18 behavioral variables (columns).

## Methods
Clustering is an unsupervised learning method that divides the feature space into clusters or groups of similar objects. In general, clustering is used for pattern recognition. In this paper, we will use two approaches for customer segmentation:
the first approach is by considering all variables for clustering algorithms using
the Hierarchical clustering and the K-means. 
The second approach is by using the dimensionality reduction through Principal Component Analysis (PCA), then identifying the optimal number of clusters, and repeating the clustering analysis with the updated number of clusters.


### First Approach: Considering All Variables for Clustering Algorithms 

####  Hierarchical Clustering
Hierarchical clustering performs a series of successive mergers to group n objects based on some distance. Unlike K-means, this method does not need clusters to be specified in advance, but rather chooses its clusters by using dendrograms [1,3,5,7,8]. A dendrogram criterion is generally used to represent the clusters, which takes the longest edge that does not cross a horizontal line as the minimum distance criterion. 
Any cluster that crosses this line will be chosen in the final model. The height of the cut to the dendrogram serves as the K value in K-means clustering:
it controls the number of clusters obtained. Hierarchical Clustering tries
to reduce the variance in the clusters [7,8,9,10,11,12].
There are two types of hierarchical clustering algorithms:
1. Agglomerative hierarchical clustering (bottom up)
2. Divisive hierarchical clustering (top down)

A distance measure defines similarity (or dissimilarity) between objects. There are different methods for calculating this distance, such as [1,3,13,14,15,16]:
The Euclidean distance - The Manhattan distance - The Minkowski distance - The Pearson sample correlation distance
There are different cluster agglomeration methods to calculate the distance
between clusters. The most common methods are [1,2,3,15,17,18,19,20,21,22]:
Maximum or complete linkage clustering - Minimum or single linkage clustering - Mean or average linkage clustering - Centroid linkage clustering - Ward’s minimum variance method.


### K-means Clustering
K-means tries to classify observations into mutually exclusive groups (or clusters), such that observations within the same cluster are as similar as possible, whereas
observations from different clusters are as dissimilar as possible.


##### Outline of the K-means Algorithm
Assuming we have input data points x1, x2, x3, …,xn and value of K (the number of clusters needed):
1. Pick K points as the initial centroids from the dataset, either randomly or the first K.
2. Find the Euclidean distance of each point in the dataset with the identified K points (cluster centroids).
3. Assign each data point to the closest centroid using the distance found in the previous step.
4. Find the new centroid by taking the average of the points in each cluster group.
5. Repeat 2 to 4 for a fixed number of iteration or till the centroids do not change.

There are several K-means algorithms available for doing this. The standard algorithm is the Hartigan-Wong algorithm, which defines the total within-cluster variation as the sum of the Euclidean distances between observation i’s feature values and the corresponding centroid :
w( ck ) = ∑ ( xi − µk)^2  
where xi is an observation belonging to the cluster Ck
µk is the mean value of the points assigned to the cluster Ck
Each observation (xi) is assigned to a given cluster such that the sum of squared (SS) distances of each observation to their assigned cluster centers (μk) is minimized.

In order to find the optimal number of clusters in K-means, it is recommended to choose it based on:
The context of the problem at hand if we know that there is a specific number of groups in our data (this option is however subjective), or with any of the following three approaches:
• Elbow method (which uses the within cluster sums of squares by looking at the total within-cluster sum of square as a function of the number of clusters. The location of a knee or elbow in the plot is usually considered as an indicator of the appropriate number of clusters),
• Average silhouette method (measures the quality of a clustering. That is, it determines how well each object lies within its cluster. A high average silhouette width indicates a good clustering),
• Gap statistic method (compares the total intra-cluster variation for different values of K with their expected values under null reference distribution of the data).



#### The Validation of Hierarchical Clustering and K-means Clustering
There are different measures for the internal validation of clustering, such as:
• Davies-Bouldin Index: considers the dispersion and separation of all clusters. The score is defined as the average similarity measure of each cluster with its most similar cluster, where similarity is the ratio of within-cluster distances to between-cluster distances. Thus, clusters which are farther apart and less dispersed will result in a better score.
• Silhouette coefficient: it lies between (-1) (e.g. poor clustering) to (+1) (e.g. good clustering). It should be maximized.
• Dunn index: It is the ratio between the smallest distance between observations not in the same cluster to the largest intra-cluster distance. It has a value between 0 and infinity and should be maximized. The higher the Dunn index value, the better is the clustering.



### Second Approach: Dimensionality Reduction Using PCA
we use PCA as an approach to group features that explain the maximum variability in the feature space.Dimensionality reduction aims to reduce the number of variables in our dataset and also reduce multicollinearity among variables.In general, a n × p data matrix (X) has min (n − 1, p) distinct principal components.We decide on the number of principal components required to visualize the data by examining a scree plot to find a point at which the proportion of variance explained by each subsequent principal component drops off. This is often referred to as
an elbow in the scree plot. Each principal component is a linear combination of the initial variables. Also, each principal component has an orthogonal relationship with each other. This means they are uncorrelated. The first principal component (PC1) captures most variability within the data. The second principal component (PC2) captures the second most. The third principal components
(PC3) captures the third most, and so on.
 ##### PCA works by
1. Normalize the Data: This is often necessary if the features in the dataset are measured in different units,
2. Calculate the covariance matrix,
3. Compute the eigen values and eigen vectors,
4. Re-orient the data,
5. Plot the data by biplots (PC1 against PC2)

Next, we apply the PCA to our dataset after normalization.

### Employing the PCA in the Clustering Analysis
 
Although PCA is mainly used for visualization and dimensionality reduction, however, it can also be employed in the clustering analysis, customer segmentation, and pattern recognition. Unlike K-means, PCA is not a direct solution for clustering, but it can be used to improve the results of the K-means clustering and the Hierarchical clustering by detecting additional clusters as compared to the optimal number of clusters in the K-means or Hierarchical clustering. Hence, we use the PCA in this paper to detect more clusters or groups and compare the results to the Kmeans and Hierarchical clustering outputs. The PCA clustering procedure is based on the 5 PCs instead of 17 variables. Applying PCA to our data frame resulted in producing 4 clusters, as shown in Figure 20 below. Since the procedure of PCA clustering produced 4 clusters, this implies that the optimal K=3 that was used in the Hierarchical and K-means has to be changed to K=4. The PCA has identified one more cluster or group of customers that was not discovered by the K-means and Hierarchical clustering. Therefore, we will update the optimal K value, and repeat the K-means clustering again to see if the results would improve with the new optimal K value.



##### Updating the K-means Clustering with K=4 instead of K=3
The new updated K-means clustering resulted in producing four principal components (or clusters or groups).

#### Characteristics of the 4 Clusters or Customer’s Groups 
By inspecting the histograms, we can interpret the
characteristics of the customers in each cluster as
follows:
1. The customers in the first cluster (cluster 0) do only one-off transaction and have least payment ratio. This group is about 21% of the total customers in the data.
2. The customers in the second cluster (cluster 1) take the maximum advance cash and pay less minimum payment and have poor credit scores. This group is about 23% of the total customers in the data.
3. The customers in the third cluster (cluster 2) have the highest monthly average purchases and they do both installments as well as one-off purchase. Besides, they generally have good credit scores. This group is about 31% of the total customers in
the data.
4. The customers in the fourth cluster (cluster 3) have maximum credit score and they pay dues and maximum installment purchases. This group is about 25% of the total customers in the data. Hence, K-means with 4 clusters is an effective tool that can show distinguished characteristics of each cluster or customer’s group.


#### Conclusions
We segmented the customers into four groups: the active users, the frequent users, the mid users, and the rare users.
the K-means better fitted with our dataset. The K-means clustering scored better than the Hierarchical clustering in terms of Davis-Bouldin, Silhouette, and Dunn index. Therefore, we conclude that the K-means clustering algorithm is more suitable for customer segmentation than Hierarchical clustering in this
dataset.unlike K-means, PCA is not a direct solution for clustering, but it can improve the results. 
unlike K-means, PCA is not a direct solution for clustering, but it can improve the results of the K-means clustering and Hierarchical clustering by detecting more clusters or patterns in the data as compared to the K-means clusters.
we saw that the procedure of PCA clustering produced 4 clusters compared to the optimal K=3 that was used in the Hierarchical clustering and Kmeans. The PCA identified one more cluster or group of customers that was not discovered by the K-means and Hierarchical clustering. Therefore, we updated the optimal K value, and repeated the K-means clustering procedure again to see if the results would improve with the new optimal K value. We showed that the new updated K-means clustering scored better than the original K-means and Hierarchical clustering in terms of Davis-Bouldin, Silhouette, and Dunn index. This implied that updating the optimal K value from K=3 to K=4 improved the outcome of K-means clustering.


Zahra Ahmadnezhad
400422011