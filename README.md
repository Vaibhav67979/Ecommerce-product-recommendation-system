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
* Solve the [Cold Start Problem](https://github.com/Vaibhav67979/Ecommerce-product-recommendation-system/blob/18d7fb2b8feafd117f7c3f9f859255c2e28cfbe4/ColdStartProblem.md)

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
* Taking the matrix of product ratings and converting it to a CSR(compressed sparse row) matrix. This is done to save memory and computational time, since only the non-zero values need to be stored.
* Performing singular value decomposition (SVD) on the sparse or csr matrix. SVD is a matrix decomposition technique that can be used to reduce the dimensionality of a matrix. In this case, the SVD is used to reduce the dimensionality of the matrix of product ratings to 50 latent features.
* Calculating the predicted ratings for all users using SVD. The predicted ratings are calculated by multiplying the U matrix, the sigma matrix, and the Vt matrix.
* Storing the predicted ratings in a DataFrame. The DataFrame has the same columns as the original matrix of product ratings. The rows of the DataFrame correspond to the users. The values in the DataFrame are the predicted ratings for each user.
* A funtion is written to recommend products based on the rating predictions made : 
  1. It gets the user's ratings from the interactions_matrix.
  2. It gets the user's predicted ratings from the preds_matrix.
  3. It creates a DataFrame with the user's actual and predicted ratings.
  4. It adds a column to the DataFrame with the product names.
  5. It filters the DataFrame to only include products that the user has not rated.
  6. It sorts the DataFrame by the predicted ratings in descending order.
  7. It prints the top num_recommendations products.
* Evaluating the model :
  1. Calculate the average rating for all the movies by dividing the sum of all the ratings by the number of ratings.
  2, Calculate the average rating for all the predicted ratings by dividing the sum of all the predicted ratings by the number of ratings.
  3. Create a DataFrame called rmse_df that contains the average actual ratings and the average predicted ratings.
  4. Calculate the RMSE of the SVD model by taking the square root of the mean of the squared errors between the average actual ratings and the average predicted ratings.

> The squared parameter in the mean_squared_error function determines whether to return the mean squared error (MSE) or the root mean squared error (RMSE). When squared is set to False, the function returns the RMSE, which is the square root of the MSE. In this case, you are calculating the RMSE, so you have set squared to False. This means that the errors are first squared, then averaged, and finally square-rooted to obtain the RMSE.
     
