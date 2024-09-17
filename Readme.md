## Person Re-Identification Problem

Approach
--------
To tackle this person re-identification problem, I’ve designed an approach that focuses on accurately grouping detections into exactly 5 distinct clusters using unsupervised clustering algorithms, each representing one individual. Here’s a step-by-step breakdown of my approach:

- Data Preparation and Feature Extraction: I started by loading the detection data and extracting the feature vectors associated with each detection. 

- Normalization: To ensure that the clustering algorithm works effectively, I normalized the feature vectors. Normalization adjusts the scale of the features, making sure that no single feature disproportionately influences the clustering process. This step is essential for improving the accuracy and performance of the clustering algorithm.

- Dimensionality Reduction with PCA: Next, I applied Principal Component Analysis (PCA) to reduce the dimensionality of the feature vectors from 768 dimensions to a more manageable 256 dimension. The reason I went with PCA is it compresses the data into fewer dimensions while preserving the most important features, so reduces the computation. Also reduction simplifies the data and can improve clustering results by removing noise and focusing on the most relevant information.

- Clustering with Gaussian Mixture Model (GMM): For the actual clustering, I used Gaussian Mixture Model (GMM). GMM is a probabilistic model that assumes data is generated from a mixture of several Gaussian distributions. It’s effective for clustering as it can capture complex patterns and variations in the data. I configured GMM to find exactly 5 clusters, aligning with our requirement to group 5 distinct individuals.

- Mapping and Saving Results: After clustering, I mapped each detection ID to its corresponding cluster label. This means that each detection ID is assigned to one of the 5 clusters. Then organized these clusters into a list format where each sublist contains detection IDs belonging to the same individual. Finally, I saved this structured information into a JSON file (prediction.json), ensured that the output matches the required format.


Custom Evaluation Technique
---------------------------
To evaluate the effectiveness of my clustering approach, I developed a custom evaluation technique. This technique compares the cluster assignments in my predictions with those in the provided ground truth data (labels.json). Here’s how it works:

- Mapping Detection IDs: I first map each detection ID to its cluster number from the predictions.
- Matching Clusters: For each group of detection IDs in the ground truth, I check if the cluster assignments from my predictions match the expected cluster. If they match, it is marked as a correct prediction.
- Accuracy Calculation: I calculate the accuracy by comparing the number of correctly matched detections to the total number of detections in the ground truth data.

Using this technique, I achieved approximately `84% accuracy` in clustering.
