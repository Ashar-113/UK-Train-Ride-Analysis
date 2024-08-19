# UK Train Ride Analysis

## Dashboard Summary
The dashboard is designed to evaluate certain aspects of the train rides across the UK. The dashboard highlights significant metrics; the percentage of delays and factors contributing to the delays. The dataset analysis indicates that 7.24% of the scheduled trains were delayed where weather conditions were a significant contributing factor followed by technical issues and signal failure. Investigating these two issues apart from the weather can yield a reduced proportion of train delays.


## Data Preparation and Modelling
The data was loaded into Power Query from a CSV file for cleaning and sorting purposes as a prerequisite for the evaluation of the dataset.

#### Data Modelling
The data model consists of a table loaded into Power BI and a measure table. A measure table is a convenient and organised way to keep our measures in a single table. The illustration below shows the data model
#
![Model](https://github.com/user-attachments/assets/faaa43eb-ca3c-400b-a59b-0597b7e19211)

#### Measure Table
Measure table is a proactive way to keep your work organised and tidy. For the analysis, the measure table consists of all the DAX expressions to evaluate the KPIs for the dashboard. For the analysis of this dashboard following DAX expressions are used:
#
**Total Revenue:** To express the total revenue that is accumulative amount from all the transactions in the dataset is expressed by the DAX expression
```
Revenue = (SUM('UK Train'[Price]))
```
**Percentage of Trains on Time:** The DAX expression to show the proportion of the trains that got on time
```
On Time % = 
 VAR a=
 CALCULATE(COUNT('UK Train'[Transaction ID]),
 'UK Train'[Journey Status] = "On Time")

 VAR b=
 COUNT('UK Train'[Transaction ID])

 VAR c= 
 DIVIDE(a,b)
 RETURN c
```
**Percentage of trains Delayed:** The key metric of this dataset is expressed by the following DAX expression
```
Delayed % = 
 VAR a=
 CALCULATE(COUNT('UK Train'[Transaction ID]),
 'UK Train'[Journey Status] = "Delayed")

 VAR b=
 COUNT('UK Train'[Transaction ID])

 VAR c= 
 DIVIDE(a,b)
 RETURN c
```
**Percentage of Cancelled:** Percentage of trains that got cancelled is evaluated by the following DAX expression
```
Cancelled % = 
 VAR a=
 CALCULATE(COUNT('UK Train'[Transaction ID]),
 'UK Train'[Journey Status] = "Cancelled")

 VAR b=
 COUNT('UK Train'[Transaction ID])

 VAR c= 
 DIVIDE(a,b)
 RETURN c
```
**Percentage of Railcard Users:** This expression gives insight into the frequent travellers using Railcard subscription
```
Railcard Users % = 
 VAR a=
 CALCULATE(COUNT('UK Train'[Transaction ID]),
 'UK Train'[Railcard] = "Adult")

 VAR b=
 CALCULATE(COUNT('UK Train'[Transaction ID]),
 'UK Train'[Railcard] = "Senior")

 VAR c= a+b

 VAR d=
 COUNT('UK Train'[Transaction ID])

 VAR e= 
 DIVIDE(c,d)
 RETURN e
```
## Dashboard Overview
Apart from the KPIs evaluated through DAX expression, the dashboard consists of other meaningful insights. The visual showing factors contributing to delay is significant in order to understand the problem. Other metrics such as peak hours and popular routes tell us about the activity on the trains and stations. Visuals that show revenue by ticket type and preferred class depict customer's preference and their purchasing behaviour.
#
![Train](https://github.com/user-attachments/assets/b0bd64e2-97c5-486b-9fde-f378f1302916)
