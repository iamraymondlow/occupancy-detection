<h1> Occupancy Detection using a Bluetooth Low Energy Approach </h1>

Among the different occupancy detection approaches, the Bluetooth Low Energy (BLE) technology has recently emerged as a popular alternative among researchers due to its availability in most smartphone devices, as well as having a low cost, low power demand, and low data latency. In this project, we will propose three different models that use a supervised Bluetooth fingerprinting approach and another model that uses a semi-supervised Bluetooth clustering approach to perform occupancy detection.

<h2>Data Description</h2>
The dataset used in this study contains a set of RSSI tuples collected using several BLE beacons deployed around an office space, labelled with the corresponding location information. However, the dataset is excluded from this repo to protect the privacy of the study participants.

<h2>Supervised Bluetooth Fingerprinting approach</h2>
<h3>Multi-class</h3>
The first model architecture resembles a multi-class classifier where each prediction class corresponds to a particular zone in the office.

<h3>Hierarchical</h3>
The second model architecture follows a hierarchical approach whereby an initial round of classification first takes place to narrow down the occupant's location to a particular area before passing the RSSI values into a second classifier which predicts the occupant's location on a zonal level based on the initial prediction.

<h3>Ensemble 1-vs-All</h3>
The third model architecture follows an ensemble 1-vs-all approach by developing a binary classifier for each zone in the study area. By comparing the probabilistic outputs of each binary classifier, the classifier with the highest probability is identified, and its corresponding location is selected as the occupant's final predicted location. However, given that there might be a considerable imbalance between the number of positive classes and negative classes when training each binary classifier, additional steps need to be taken when developing the ensemble model. The issue of class imbalance is overcome by splitting the data in the negative class into multiple batches, where the size of each batch equals to the number of data points in the positive class. By combining each batch containing the negative class with the data from the positive class, a binary classifier is trained on each resulting dataset. Given that the classifier for each zone is made up of an ensemble of binary classifiers, the combination of classifiers from each zone results in an ensemble model of ensemble models.

<h2>Semi-supervised Bluetooth Clustering approach</h2>
The second machine learning approach proposed in this paper follows a semi-supervised approach that combines the use of the K-means clustering algorithm, together with a small amount of labelled data, to perform occupant localisation. However, given that the K-means algorithm is only able to provide a numerical label to the data points that belong to the same cluster, an additional step is needed to map each cluster label to a particular zone in the study area. This mapping step is achieved by collecting a small sample of labelled data from each zone (for instance, ten data points per zone), and calculating the centroid of these labelled samples.Next, by calculating the Euclidean distance between a labelled centroid and the cluster centroids, we identify the nearest cluster centroid and assign the corresponding zone label to the data points in that cluster. Additional steps were also taken to ensure that each zone is uniquely mapped to a particular cluster. 

As the initial K centroids are randomly selected from the dataset, different initialisation of the K centroids might result in different cluster labels for the same data point, leading to large fluctuations in model performance. This issue has been overcome by initialising the K-means algorithm with the labelled centroids described earlier to ensure that the algorithm produces similar predictions every time the clustering algorithm is rerun. Furthermore, by initialising the clustering algorithm with the labelled centroids, convergence time should also decrease accordingly.
