# Predicting Lake Berryessa Water Level Using Machine Learning 
By Steven Chen, Jason Wu, Young Cheol Ko, Joshua Buhain, Rohith Kolli

## Abstract
Our project will be taking collected water reservoir data in California to create a regression to predict future water levels. It will highlight the differing various changes of Lake Berryessa by their reservoir storage, inflow and outflow. A reliable prediction model will help aid in better planning and mitigations of risks such as droughts. The data in observation will be taken from 2001 to 2021. Those are the years which we look at.

## Introduction
California is experiencing its driest three-year period on record, and the fourth year of drought is forecasted. One of the most drastic consequences of such extreme drought conditions is diminishing freshwater supplies. Reservoirs are an important source of water for both agricultural and urban usage. They furthermore provide flood control, recreation, wildlife habitat, and hydropower benefits.

The height of the reservoir water level has far-reaching consequences. Too low and farmers might be forced to leave their lands uncultivated, hydropower is not generated, and citizens experience water insecurity. Too high and adequate flood protection is at stake. Therefore, predicting reservoir water level is crucial to prepare for future conditions and mitigate potential negative consequences.

California has about 1,300 reservoirs that can hold more than 43 million acre-feet of water. One of these reservoirs is Lake Berryessa, located west of Davis. It provides agricultural water to farmland in Solano County and municipal and industrial water to the county’s cities. Like the majority of reservoirs in the State, Lake Berryessa is at a low point compared to historical levels; it is currently down to 395 feet, the lowest it has been since 1995. 

The purpose of the current project is to build a model that predicts Lake Berryessa reservoir water level. Data regarding Lake Berryessa reservoir is publicly available on the California Department of Water Resources website and can be scraped manually using their web API.

Lake Berryessa, 3/14/2015
![lake-berryessa-mark-ruanto](https://user-images.githubusercontent.com/68248379/205460300-15a55755-6e26-4f8e-a519-8cc007c06576.jpg)

Lake Berryessa, 10/22/2022
![IMG_7716](https://user-images.githubusercontent.com/68248379/205460106-9a615ddd-ec54-4405-9a0b-473f6c67f3f7.jpg)

## Data Exploration
We requested our dataset from the California Department of Water Resources data center [(Link)](https://cdec.water.ca.gov/dynamicapp/staMeta?station_id=BER). The department installed various kinds of sensors in the reservoir and collected data related to the reservoir. These various types of data are used by them to manage the water resources of the reservoir. This data is publicly available to everyone to help researchers in monitoring the various lakes in California. This site makes data easy to read and understand by giving a graph display as well as tables. In our case, we requested to use data about Lake Berryessa about its daily inflow, outflow, precipitation, and water storage from 2001 to 2021. 

![heatmap](https://user-images.githubusercontent.com/68248379/205461165-33ede1b7-c13a-4dbd-98c0-8f5576523f84.JPG) Format: ![Alt Text]



## Data Preprocessing 
The data measurements gathered from CDWR data center are updated daily with a few null values. We don’t think we have imbalanced data as they are recorded daily and were all under the same time frame. Our pair plots do not indicate dramatic outliers in our dataset, . To account for the oddities in our data set, null values and “---” were removed from the dataset. Date and time were converted from their string value to a Date object to be used in matplotlib. For example, the original string of “20010101 0000” was converted into a more usable “010101” to represent January 1st, 2001. We then subtract each date object with the date of the first row to turn them into days elapsed. Data values for inflow and outflow categories were normalized to make the display of the incredibly large values less varying. To get an estimation of the distribution of data, we created a polynomial regression prediction of water storage level changes by time. 


## Model Design

### Model 2: Neural network 
Our goal with the neural network is get the train data of one year and try to predict the next year of storage level. First, we divided our data from 0 to 365 to get first year of the data. Our test data is the whole next year's storage value. We created a neural network model with the keras neural network. And we added multiple layers with different functions (relu, tanh, sigmoid). We tried 3 different function combination models. But, It showed that any combination of different function models gives the same percentage error around 0.5.

## Conclusions



# Colab Link
https://colab.research.google.com/drive/1YLEEMDktyVtE5MWI_Y_atUegwV3mt5jd#scrollTo=h5cYFrr600Zv
