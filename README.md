# Predicting Lake Berryessa Water Level Using Machine Learning 
By Steven Chen, Jason Wu, Young Cheol Ko, Joshua Buhain

## Introduction
California is experiencing its driest three-year period on record, and the fourth year of drought is forecasted. One of the most drastic consequences of such extreme drought conditions is diminishing freshwater supplies. Reservoirs are an important source of water for both agricultural and urban usage. They furthermore provide flood control, recreation, wildlife habitat, and hydropower benefits.

The height of the reservoir water level has far-reaching consequences. Too low and farmers might be forced to leave their lands uncultivated, hydropower is not generated, and citizens experience water insecurity. Too high and adequate flood protection is at stake. Therefore, predicting reservoir water level is crucial to prepare for future conditions and mitigate potential negative consequences.

California has about 1,300 reservoirs that can hold more than 43 million acre-feet of water. One of these reservoirs is Lake Berryessa, located west of Davis. It provides agricultural water to farmland in Solano County and municipal and industrial water to the county’s cities. Like the majority of reservoirs in the State, Lake Berryessa is at a low point compared to historical levels; it is currently down to 395 feet, the lowest it has been since 1995. 

The purpose of the current project is to build a model that predicts Lake Berryessa reservoir water level. Data regarding Lake Berryessa reservoir is publicly available on the California Department of Water Resources website and can be scraped manually using their web API.

Lake Berryessa, 3/2015
![lake-berryessa-mark-ruanto](https://user-images.githubusercontent.com/68248379/205460300-15a55755-6e26-4f8e-a519-8cc007c06576.jpg)

Lake Berryessa, 11/2022
![IMG_7716](https://user-images.githubusercontent.com/68248379/205460106-9a615ddd-ec54-4405-9a0b-473f6c67f3f7.jpg)

## Data Exploration
We requested our dataset from the California Department of Water Resources data center [(Link)](https://cdec.water.ca.gov/dynamicapp/staMeta?station_id=BER). The department installed various kinds of sensors in the reservoir and collected data related to the reservoir. These various types of data are used by them to manage the water resources of the reservoir. This data is publicly available to everyone to help researchers in monitoring the various lakes in California. This site makes data easy to read and understand by giving a graph display as well as tables. In our case, we requested to use data about Lake Berryessa about its daily inflow, outflow, precipitation, and water storage from 2001 to 2021. 

![heatmap](https://user-images.githubusercontent.com/68248379/205461165-33ede1b7-c13a-4dbd-98c0-8f5576523f84.JPG)



## Data Preprocessing 

<img width="1176" alt="Screen Shot 2022-12-04 at 12 50 26 AM" src="https://user-images.githubusercontent.com/31902338/205481990-893f357d-c7ce-4631-b454-966376a740cf.png">

- We dropped the following columns from our CSV:
    - Station_ID: All measurements originate from the same station ID 
    - DATA_FLAG: There is actually no data under this column
    - DURATION: All our dataset is recorded daily (D). Redundant.
    - UNITS: Redundant.
    - OBS DATE: This column is redundant, exactly the same as Date Time.
- We don’t think we have an imbalanced dataset as each data column was consistently recorded daily and were all under the same time frame.
- However, some of the data measurements gathered from CDWR data center are updated daily with a few null values. 
- To account for the oddities in our data set, null values and “---” were removed from the dataset.
- We processed Date and time in two ways
    - Converted from their string value to a Date object to be used in matplotlib. For example, the original string of “20010101 0000” was converted into a Date object. We omitted the last 4 digits as it is reserved for hours and minutes.
    - Further added two new columns, one that shows days elapsed since the start of our data set. Populated by subtracting current date with initial date. And another that shows which day of the year it is.
- Data values for inflow and outflow categories were normalized to make the display of the incredibly large values less varying. 

Processed Date Time
<img width="510" alt="Screen Shot 2022-12-04 at 12 57 14 AM" src="https://user-images.githubusercontent.com/31902338/205482298-fe4cc55a-4c12-4149-9872-7845bbdd1676.png">

Normalized data for relevant columns
<img width="459" alt="Screen Shot 2022-12-04 at 12 59 28 AM" src="https://user-images.githubusercontent.com/31902338/205482352-14241fed-dc8d-4ed1-af5e-723b3f54ffed.png">


## Model Design
### Model 1: Polynomial Regression 
Before creating the model, we created a polynomial regression of degree 4 for both a 20-year dataset and a single year dataset to help visualize the dataset. It seemed to be a decent fit compared to a linear or logistic regression, with a training MSE of approximately .00304 and a testing MSE of approximately .00227.

Our polynomial regression model had a training mean-squared error (MSE) of about .0334 and a testing MSE of .0345, which are good values. Our training and testing R squared error was -.335 and -.375. 

![a1](https://user-images.githubusercontent.com/68248379/205481573-01880839-6ee3-486a-827d-f6542edb714b.JPG)
![a2](https://user-images.githubusercontent.com/68248379/205481578-467bf512-3f9b-4b08-8c43-b42b23238a3c.JPG)

### Model 2: Neural network 

Our goal with the neural network is to get the train data(the inflow, outflow, precipitation, date of the year, and storage change) of one year and try to predict the next year of storage level. First, we divided our data from 0 to 365 to get the first year of the data. Our test data is the whole next year's storage value. We created a neural network model with the keras neural network. And we added multiple layers with 4 different activation functions (relu, tanh,and sigmoid). We tried three different function combination models: the only using relu with sigmoid, one tanh and two relu with sigmoid, and lastly, two tanh and one relu with sigmoid.  But, It showed that any combination of different function models gives the same percentage error around 50%. It will consider the prediction to be correct if it is within 5% of error from the actual value.

![model1](https://user-images.githubusercontent.com/68248379/205481763-6f77d1e8-1364-4934-965a-660c34816444.PNG)

## Discussion
In this assignment, we ran into many problems that may have led to skewed results. For one case, Lake Berryessa is a unique lake with a very distinct feature called the “hole”. This hole is a giant water spillway that will drain the excess water when the reservoir’s storage hits the capacity.  This spillway is why we see a massive increase in the ‘outflow’ when the water level is high, and why ‘outflow’ has some correlation with the storage, but has little correlation with ‘storage change.’  This is the main reason why we have trouble predicting the ‘storage change,’ and how the ‘storage change’ has almost no correlation with the ‘storage.’

Similarly, we did not have enough sensor data to work with to help make an accurately predictive model for neural networks. The majority of the water would come from rainfall, and exit through vaporization or infiltration, those are not included in the ‘Inflow’ and ‘outflow.’ Which is the reason why they both have little correlation with ‘storage’ 

Another conditional issue related is that water level is incredibly dependent on the seasonal changes. Using random train and test values, while key in neural networks would not be possible with the varying water levels based on the season of the year. A solution to this issue would possibly be to have a constant model that can modify itself based on its current season. 

While it may be possible to resolve these problems if we used a different set of neural nodes to calculate our values, or do more processing with our data. 


## Conclusions
Lake Berryessa is a breathtaking natural landscape filled with plenty of unique wildlife and scenery. In order to best understand its majestic beauty, our group took a field trip to observe the shining blue lake itself. 

With our current training model, we have a relatively effective predictive model that can estimate Lake Berryessa’s storage capacity over a yearly basis. If given a possible second chance on the project, we would probably pick another fantastic lake like Lake Tahoe to describe changing water levels. It also might be possible that an SVM would be a more effective approach to calculating an estimate of changes since water storage is never a set amount and is ever changing depending on the year. 

In conclusion, our project attempts to predict Lake Berryessa’s changing water levels by Neural Network and Polynomial regression. While our model is not as accurate as we hoped it be, we hope it is an introductory step creating a machine learning prediction model. 

Below attached is an image of our group visit to Lake Berryessa, a local landmark less than 15 miles away from UC Davis!

![IMG_5028](https://user-images.githubusercontent.com/68248379/205481726-651222c3-d07b-468b-ac5c-d83aeee8ac5e.jpg)



# Colab Link
https://colab.research.google.com/drive/1YLEEMDktyVtE5MWI_Y_atUegwV3mt5jd#scrollTo=h5cYFrr600Zv
