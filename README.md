# Water-Level Project 
By Steven Chen, Jason Wu, Young Cheol Ko, Joshua Buhain, Rohith Kolli

# Abstract
Our project will be taking collected water reservoir data in California to create a regression to predict future water levels. It will highlight the differing various changes of Lake Berryessa by their reservoir storage, inflow and outflow. A reliable prediction model will help aid in better planning and mitigations of risks such as droughts. The data in observation will be taken from 2001 to 2021. Those are the years which we look at.

#Introduction
California is experiencing its driest three-year period on record, and the fourth year of drought is forecasted. One of the most drastic consequences of such extreme drought conditions is diminishing freshwater supplies. Reservoirs are an important source of water for both agricultural and urban usage. They furthermore provide flood control, recreation, wildlife habitat, and hydropower benefits.

The height of the reservoir water level has far-reaching consequences. Too low and farmers might be forced to leave their lands uncultivated, hydropower is not generated, and citizens experience water insecurity. Too high and adequate flood protection is at stake. Therefore, predicting reservoir water level is crucial to prepare for future conditions and mitigate potential negative consequences.

California has about 1,300 reservoirs that can hold more than 43 million acre-feet of water. One of these reservoirs is Lake Berryessa, located west of Davis. It provides agricultural water to farmland in Solano County and municipal and industrial water to the county’s cities. Like the majority of reservoirs in the State, Lake Berryessa is at a low point compared to historical levels; it is currently down to 395 feet, the lowest it has been since 1995. 

The purpose of the current project is to build a model that predicts Lake Berryessa reservoir water level. Data regarding Lake Berryessa reservoir is publicly available on the California Department of Water Resources website and can be scraped manually using their web API.

# Preprocessing Data (Plan)
We will be normalizing the data as there is not much correlation and the graphs are skewed and not normal between Inflow, Outflow and Storage. We will modify our time frame to be more appropiate such as tracking monthly and/or yearly instead of daily to limit variance and for a more accurate representation of the seasons. 


# Preprocessing Data (After)
We encoded date/time values from 0 to 4000. We normalized our data to make it more readable. We used 'DATE TIME' as x-axis and 'STORAGE' as our y-axis for our linear & polynomial regressions as we are trying to predict future water storage over time. Linear regression was an incredibly poor fit, so we decided that our polynomial regression model with the 9th degree has the best represents our prediction. The graph is an underfit graph since it cannot accurately predict the natural occurances such as drought and heavy rain seasons. The MSE for test and training is printed out below the graphs of each one.

Upcoming changes: We need to convert date time from an encoded string to a date time object with python for a more smooth graph. Scale the data by yearly to see how it changes by year.


# Colab Link
https://colab.research.google.com/drive/1YLEEMDktyVtE5MWI_Y_atUegwV3mt5jd#scrollTo=h5cYFrr600Zv
