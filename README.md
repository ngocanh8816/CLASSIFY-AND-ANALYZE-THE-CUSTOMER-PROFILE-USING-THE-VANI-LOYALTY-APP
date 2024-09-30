# CLASSIFY AND ANALYZE THE CUSTOMER PROFILE USING THE VANI LOYALTY APP
Classify customers based on the entire application using RFM, Cohort Analysis and Churn Analysis techniques. From there, create a detailed customer profile to help the Marketing department implement appropriate promotional programs.

# Overviews
The analysis project covers the following areas:

+ **Data collection**: Use internal datasets aggregated from recording and responding to user activities within the application.
+ **Data preparation**: Cleaning and preprocessing the data for analysis.
+ **Descriptive analytics**: Calculate the necessary metrics for the analysis.
+ **Diagnostic analytics**: Identify and analyze the root causes of issues found in past data.
+ **RFM analysis**: Classify and segment customers into appropriate groups using specific RFM criteria.
+ **Cohort analysis**: Classify customers by specific time periods and analyze customer retention rates by cycle.
+ **Churn analysis**: Analyze customer churn rates when using the service.
+ **Propose solutions**: Identify and propose some solutions to improve the operations of the marketing department at the company

# Applied Skills
ETL Data, EDA Data, Data Analysis, Data Visualization (using Python)

# Key Features
+ **Data preparation**: Identify the necessary information fields for the analysis process, while also converting and formatting the time data type. Specifically, filter out the data on successful transactions when customers use the application.
+ **Transform data**: Calculate the necessary customer metrics, average number of transactions, customer retention rate and service churn rate, etc.
+ **Data analysis**: Apply the RFM method to classify customers and use Cohort and Churn analysis to better understand customer behavior and the application’s performance.
+ **Data visualization**: Use two visualization libraries, Matplotlib and Seaborn, in Python to represent and extract useful information from the data.

# Key Findings
**RFM Analysis**

Classify all customers who have used and are using the loyalty services to help the marketing department capture their characteristics, quantity, and activity indicators over time.

**Cohort Analysis**

Classify specific customer groups based on the first time they made a transaction. By monitoring each cycle, the marketing department can identify when changes in customer behavior occur and apply appropriate solutions. Additionally, this analysis method helps to evaluate the overall potential of the loyalty program and the overall performance of each related business brand.

**Churn Analysis**

Provide the most comprehensive overview for base managers about customer churn over time.

Additionally, combine this with the results from RFM analysis to better illustrate the profiles of three common customer segments. From there, propose a few solutions that the marketing department can use to continue focusing on maintaining and exploiting these potential customer segments.
# Outcomes
**Assessment and a few action suggestions**

*'Champions' Segment*
+ Customers in the Champions segment have a gradually decreasing churn rate that remains relatively stable during the business period. This indicates that customers in this segment are very loyal and have a low tendency to leave the service. The stability in the churn rate shows that they are less affected by minor changes in service or pricing.

+ For this potential customer segment, the company’s marketing activities should implement loyalty programs and personalize the experience for each customer in this segment to maintain long-term relationships.

*'Cannot Lose Them' Segment*
+ For customers in the “Cannot Lose Them” segment, they previously had a history of frequent app usage and accumulated points above the average level. However, by March 2023, their churn rate showed an increasing trend, indicating they were not returning to use the app.
  
+ Therefore, in the future, it is necessary to forecast the times when the churn rate of this customer segment increases. Based on these forecasts, the marketing department should plan to retain them through various methods such as creating more interaction opportunities, extending point accumulation offers, etc.

*'About To Sleep' Segment*
+ The “About To Sleep” customer segment had a relatively stable and low churn rate from January 2023 to around January 2024. However, there was a significant increase in April 2021, followed by a return to low and stable levels from April 2023 onwards, possibly due to an event or change that affected customer behavior. The sudden increase in April 2023 indicates that customers in this segment may be sensitive to major changes or special events. This could include changes in pricing, service quality, or other external factors. If no unexpected events occur, customers in this segment are likely to continue maintaining stable behavior and low churn rates.

+ To continue retaining and leveraging this customer segment, the company’s marketing department should implement reminder messages or special offers to encourage customers to increase their service usage frequency.
# Example Code
```
# Import thư viện
import pandas as pd
import numpy as np
import datetime as dt
from google.colab import drive
drive.mount('/content/drive/')


# Đọc file transfer_menbership_transaction
trans = pd.read_csv('/content/drive/My Drive/TC-BI69-Group 2/Slide + Record/RFM + Churn + Cohort/transfer_membership_transaction.csv')


# Chuyển đổi kiểu dữ liệu cho cột
## membership_transaction_time -> datetime
trans['membership_transaction_time'] = pd.to_datetime(trans['membership_transaction_time'],format='mixed')
## product_purchase_time -> datetime
trans['product_purchase_time'] = pd.to_datetime(trans['product_purchase_time'],format='mixed')
## created_at -> datetime
trans['created_at'] = pd.to_datetime(trans['created_at'],format='mixed')
## modified_at -> datetime
trans['modified_at'] = pd.to_datetime(trans['modified_at'],format='mixed'

# Lọc ra những giao dịch bị CANCEL
trans['cancel_count'] = trans.sort_values(['membership_transaction_no','org_membership_transaction_no'],ascending=[True,False]).groupby(['user_id','org_membership_transaction_no']).cumcount()+1
demen_trans = trans.groupby(['user_id','org_membership_transaction_no'])['cancel_count'].max().reset_index()
result = pd.merge(trans,demen_trans,on=['org_membership_transaction_no','user_id'],how='inner',suffixes=('_x', '_y'))
final_result = result[result['cancel_count_y'] <= 1]
```
# Project Structure
The project includes the following main components:

+ `README.md`: This file provides information and an overview of the analysis.
+ `Classify and Analyze The Customer Profile Using The VANI Loyalty App`: The Google Colab file contains code for processing, transforming, and retrieving data.
