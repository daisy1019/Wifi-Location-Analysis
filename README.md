**Statement of Goals**

This report is aiming to find the best indoor Wi-Fi location technique to navigate people  without getting lost in a complex, unfamiliar interior space such as in large industrial campuses, shopping malls etc..  We have been provided with a large database of Wi-Fi fingerprints for a multi-building industrial campus to study and provide the best indoor Wi-Fi location for clients. 



**Description and Location of the Data**

**Location** - The dataset is obtained from UCI Machine Learning Repository website, and saved into R studio.

**Description** - The dataset contains 2 data files: trainingData (19937 rows) for training predictive models, validationData (1111 rows )for doing predictions based on trained models. They have the following attributes:
520 Wi-Fi fingerprints that are characterized by the detached Wireless Access Points (WAPs) and the corresponding Received Signal Strength Intensity (RSSI). Intensity value for WAP520. Negative integer values from -104 to 0 and +100. Positive value 100 used if WAP520 was not detected
Longitude (negative values) / Latitude (positive values)
Floor - integer values 0-4
Building ID - categorical integer values 0-2
Space ID - internal space in a building, categorical integer values 1-254
RelativePosition - 1- Inside, 2- Outside
User ID - user identifier, categorical integer values 1-18
Phone ID - android device & version, categorical integer values 1-24
Timestamp - unix time of capture taken, integer values. 


**Predictive Model Building and Evaluation**

**Model Comparison**

Three models were selected for training predictive models on three separate buildings: KNN (K Nearest Neighbors), RF (Random Forest) and C50. There is another model SVM (Support Vector Machine) was trained for Builging 0 $1 as well, it took the longest time and yielded the lowest accuracy score, therefore I didnt continue using that model for Builging 3. The dataset was spilt into 75% for traing / testing set, the remaining 25% for prediction set, 10 fold cross validation was also used during the training process to generate the training score and process time. Below graphs show the training scores and process time:

![image](https://user-images.githubusercontent.com/80385435/188073107-86cc1fed-5a03-47e6-91b8-c0365bade9d3.png)

![image](https://user-images.githubusercontent.com/80385435/188073165-0d88d012-f529-4fb0-9a86-bbfe61a5aafb.png)

![image](https://user-images.githubusercontent.com/80385435/188073227-9f27b2b4-1436-489e-84de-f8f716593e12.png)

KNN model generated the fastest speed but lowest Accuracy and Kappa score.

Building 0 - C50 was chosen for best training model due to its highest Accuracy and Kappa score, with tuning parameters trials = 20, model = rules, winnow = false.
Building 1 - RF was selected as it yielded the highest Accuracy and Kappa value with mtry = 233.
Building 2 - RF was selected with highest Accuracy and Kappa value with mtry = 233.


**Resamples() Function**

The resamples() function was used to generate Accuracy and Kappa score for different building from min - max, the figures were close to values obtained from training dataset, which interprets the reliability of these training values obtained.


![image](https://user-images.githubusercontent.com/80385435/188073523-ce0454ec-54f6-4cfa-a81e-137fc0ae7feb.png)


**Visualization for Training Models**

Below graphs show similar tendency for training set as the scores were close to one another. 


Building 0 - C50                                          Building 1 - RF                                    Building 2 -  RF

![image](https://user-images.githubusercontent.com/80385435/188073645-58cbbc92-9061-44a1-812e-67801c62c401.png)
![image](https://user-images.githubusercontent.com/80385435/188073673-2f27af29-157d-4dee-943c-836b59f004ad.png)
![image](https://user-images.githubusercontent.com/80385435/188073690-69364854-6448-4316-a42b-c0339f8e01f8.png)


**Conclusions and Recommendations**


Large scale deployment of indoor location awareness is much more difficult due to complicated indoor environments such as building geometries, the movement of people, the random effects of signal propagation, interference and noise from other devices, all these factors can affect the accuracy of indoor signal positioning. A Wi-Fi based indoor positioning system that includes an integrated human-centric collaborative feedback model can be introduced to improve the accuracy of indoor Wi-Fi locationing. 

Three types of feedback can be proposed:
Positive feedback is generated when users reject the estimated position and suggest a location based on their knowledge. In such a case, the system can accept the updated information from the users.
Negative feedback indicates that the users do not believe the estimated position, and are unable to make any suggestion as to their current location. In this case, the system should reduce the positioning likelihood of the returned location in the future.
Null feedback occurs when users choose not to provide any feedback. The assumption here is that the estimated position is accurate, and that there is no need to make any modification to the positioning model. 



