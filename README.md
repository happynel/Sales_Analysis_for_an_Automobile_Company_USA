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

![Data Science Project 1 _Data Reading](https://github.com/user-attachments/assets/810bbd82-f823-4e83-a79c-f57d540222a9)


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

![Data sceince project 1_Data Modification](https://github.com/user-attachments/assets/6ffdd1e6-39d5-4ddd-9202-f95c1061cccf)


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


![Data Science Project 1 _Data filtering](https://github.com/user-attachments/assets/29893aa2-6a3d-49c9-a4a1-75932bb6986f)


#### Data Aggregation
```Python
#Aggregating the total profit by United states for bikes sales 

#solution

top_most_5 = top_most_5.pivot_table(values = "Profit", index = "CustomerState", aggfunc = np.sum)
top_most_5
```


![Data Science Project 1 _Data Aggregation](https://github.com/user-attachments/assets/c22f0537-ee29-4654-8ea4-4d60f7659cb0)


#### Data Sorting
```Python
# Sorting the aggregated data,
# in order to rank the top 5 most profitable states in USA 

# Solution 

top_most_5_states = top_most_5.sort_values("Profit", ascending = False)
top_most_5_states
```

![Data Science Project 1 _Data sorting](https://github.com/user-attachments/assets/c384b955-04de-4835-88b0-ded7e3e443c7)


#### Result
```Python
# The Top Most-Profitable 5 States for the Bike product category in the United States

# Solution

top_most_5_states.head()

most_profitable_5_US_states = top_most_5_states.head()
most_profitable_5_US_states
```

![Data Science Project 1 _Result](https://github.com/user-attachments/assets/93cc94ff-d79a-48d2-be55-4282ee8725d8)

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

![Data science project 1 screenshot](https://github.com/user-attachments/assets/56ab2c57-76bf-4cbc-be33-0800698a7fdb)

















