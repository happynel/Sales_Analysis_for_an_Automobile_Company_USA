# Sales_Analysis_for_an_Automobile_Company_USA
A Data Science Project that Analysed  the sales performance of an Automobile company Based in the United States. The company’s sales transaction data generated over the past years was used for this  analysis.

## PROBLEM STATEMENT:
What are the Top Most-Profitable 5 States for the Bike product category in the United States ?

## DATA PRE-PROCESSING
#### DATA LOADING
```Python
# Importing all necessary packages 

# Solution 

import pandas as pd
import numpy as np 
import matplotlib.pyplot as plt


print ("Packages Import;SUCCESSFUL")
```


```Python
# reading the sales data into the pandas dataframe

# Solution

bikes_df =  pd.read_csv("C:/Users/HP/Desktop/_EXCLUSIVE DATA SCIENCE BOOT CAMP_STUDENT FOLDER/_DATASET/bikes.csv")
bikes_df.head()
```

#### Data Modification
```Python
# Adding the following 3 columns; TotalCostPrice, SalesRevenue, Profit.

# TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)
bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 

# SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)
bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 

# Profit : To be obtained by (SalesRevenue - TotalCostPrice)
bikes_df["Profit"] = bikes_df["SalesRevenue"] - bikes_df["TotalCostPrice"]
bikes_df.head()
```

## DATA ANALYSIS
## Data Filtering 
```Python
# Filtering out only the data relevant to solving the problem statement 

is_a_usa = bikes_df["CustomerCountry"] == "United States"
is_bike = bikes_df["ProductCategory"] == "Bikes"

bikes_df[(is_a_usa) & (is_bike)]

top_most_5 = bikes_df[(is_a_usa) & (is_bike)]
top_most_5
```

#### Data Aggregation
```Python
#Aggregating the total profit by United states for bikes sales 

#solution

top_most_5 = top_most_5.pivot_table(values = "Profit", index = "CustomerState", aggfunc = np.sum)
top_most_5
```

#### Data Sorting
```Python
# Sorting the aggregated data,
# in order to rank the top 5 most profitable states in USA 

# Solution 

top_most_5_states = top_most_5.sort_values("Profit", ascending = False)
top_most_5_states
```

#### Result
```Python
# The Top Most-Profitable 5 States for the Bike product category in the United States

# Solution

top_most_5_states.head()

most_profitable_5_US_states = top_most_5_states.head()
most_profitable_5_US_states
```


## DATA VISUALIZATION
```Python
most_profitable_5_US_states.plot(kind = "bar")

#Adding a title and label to the plot 
plt.title("The Top 5 Most Profitable States for Bikes Product in USA")

#Labelling 
plt.ylabel("Total Profit in Milion Dollars")
plt.xlabel("States")

# Showing the plot
plt.show()
```




















