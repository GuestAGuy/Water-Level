# Water-Level Project 
By Steven Chen, Jason Wu, Young Cheol Ko, Joshua Buhain, Rohith Kolli

# Abstract
Our project will be taking collected water reservoir data in California to create a regression to predict future water levels. It will highlight the differing various changes of a Lake Berryessa by their reservoir storage, inflow and outflow. A reliable prediction model will help aid in better planning and mitigations of risks such as droughts. The data in observation will be taken from 2001 to 2021.

# Preprocessing Data (Plan)
We will be normalizing the data as there is not much correlation and the graphs are skewed and not normal between Inflow, Outflow and Storage. We will modify our time frame to be more appropiate such as tracking monthly and/or yearly instead of daily to limit variance and for a more accurate representation of the seasons. 


# Preprocessing Data (After)
We encoded date/time values from 0 to 4000. 
We normalized our data to make it more readable. 
We used 'DATE TIME' as x-axis and 'STORAGE' as our y-axis for our linear & polynomial regressions as we are trying to predict future water storage over time. 
We decided that our polynomial regression model best represents our prediction. 
