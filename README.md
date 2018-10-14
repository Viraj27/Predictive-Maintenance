
# Predictive Maintenance

A project which incorporates Machine Learning algorithms to identify which in-service machine is in risk of failing so that necessary maintenance can be provided for those machines.

## Dataset

The dataset has been taken from [https://gallery.azure.ai/Collection/Predictive-Maintenance-Template-3].(https://gallery.azure.ai/Collection/Predictive-Maintenance-Template-3) The description for the dataset is also present there.

### Training Data:

The training data consists of multiple multivariate time series with "cycle" as the time unit, together with 21 sensor readings for each cycle. Each time series can be assumed as being generated from a different engine of the same type. Each engine is assumed to start with different degrees of initial wear and manufacturing variation, and this information is unknown to the user. In this simulated data, the engine is assumed to be operating normally at the start of each time series. It starts to degrade at some point during the series of the operating cycles. The degradation progresses and grows in magnitude. When a predefined threshold is reached, then the engine is considered unsafe for further operation. **In other words, the last cycle in each time series can be considered as the failure point of the corresponding engine.**

### Test Data:

The testing data has the same data schema as the training data. The only difference is that the data does not indicate when the failure occurs. Taking the sample testing data shown in the following table as an example, the engine with id=1 runs from cycle 1 through cycle 31. It is not shown how many more cycles this engine can last before it fails.

### Ground- Truth Data:

The ground truth data provides the number of remaining working cycles for the engines in the testing data. Taking the sample ground truth data shown in the following table as an example, the engine with id=1 in the testing data can run another 112 cycles before it fails.

## Workflow

### 1. Importing the Dataset into a CSV format

###  2. Data Labeling

2 columns (Label1 and Label2) are used as markers to indicate whether the machine RUL is below a specified value. 2 constants, W1 and W0 have been defined to portray those values. These constants serve as classifiers to identify whether that an engine id, for a particular RUL will be classified as a 0 or 1 (Binary classification) or as 0/1/2 (Multi-Class). 
For example, W1 = 10 and W2 = 20. For Binary classification, whenever RUL > 20, The **Label1** column will have 0. When RUL drops below 20, the column will have 1. 
Similarly, For Multi-Class classification, whenever 20 < RUL < 10, **Label2** column will have 1. When RUL < 10, the column will have 2.  

A similar labeling approach has been implemented for test data as well based on the ground-truth values.

### 3. Normalizing Data

All the columns which contained sensor values for the engine were normalized. Min-Max normalization was applied.m

All the sensor value columns for the test data were also normalized

### 4. Preparing the Test Data

The test data will contain of a 100 rows, 1 row for each Engine ID with the maximum cycle value. This data is then appended with the Ground Truth data containing RUL, Label1 & Label2 values.

### 5. Binary Classification

3 Machine Learning algorithms have been used to juxtapose the results obtained on creating the 3 models. They were Logistic Regression, Random Forests and Neural Networks.

### 6. Multi-Class Classification

Neural Networks and Logistic Regression were used to train the dataset.
