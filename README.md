# Ecommerce-product-recommendation-system

Product Recommendation System is a machine learning-based project that provides personalized product recommendations to users based on their browsing and purchase history. The system utilizes collaborative filtering and content-based filtering algorithms to analyze user behavior and generate relevant recommendations. This project aims to improve the overall shopping experience for users, increase sales for e-commerce businesses

## Dataset

I have used an amazon dataset on user ratings for electronic products, this dataset doesn't have any headers. To avoid biases,  each product and user is assigned a unique identifier instead of using their name or any other potentially biased information.

* You can find the [dataset](https://www.kaggle.com/datasets/vibivij/amazon-electronics-rating-datasetrecommendation/download?datasetVersionNumber=1) here - https://www.kaggle.com/datasets/vibivij/amazon-electronics-rating-datasetrecommendation/download?datasetVersionNumber=1 

* You can find many other similar datasets here - https://jmcauley.ucsd.edu/data/amazon/


## Approach

### **1) Rank Based Product Recommendation**
Objective -
* Recommend products with highest number of ratings.
* Target new customers with most popular products.

Outputs -
* Recommend top 5 products with 50/100 minimum ratings/interactions.

Approach -
* Calculate average rating for each product.
* Calculate total number of ratings for each product.
* Create a DataFrame using these values and sort it by average.
* Write a function to get 'n' top products with specified minimum number of interactions.


### **2) Similarity based Collaborative filtering**
Objective -
* Provide personalized and relevant recommendations to users.

Outputs -
* Recommend top 5 products based on interactions of similar users.

Approach -
* Here, user_id is of object, for our convenience we convert it to value of 0 to 1539(integer type).
* We write a function to find similar users - 
  1. Find the similarity score of the desired user with each user in the interaction matrix using cosine_similarity and append to an empty list and sort it.
  2. extract the similar user and similarity scores from the sorted list 
  3. remove original user and its similarity score and return the rest.
* We write a function to recommend users - 
  1. Call the previous similar users function to get the similar users for the desired user_id.
  2. Find prod_ids with which the original user has interacted -> observed_interactions
  3. For each similar user Find 'n' products with which the similar user has interacted with but not the actual user.
  4. return the specified number of products. 

### **3) Model based Collaborative filtering**
Objective -
* Provide personalized recommendations to users based on their past behavior and preferences, while also addressing the challenges of sparsity and scalability that can arise in other collaborative filtering techniques.

Outputs -
* Recommend top 5 products for a particular user.

Approach -
* 
* 
* 

