# Credit Card Financial Dashboard using Power BI:

# Project Objective
To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.

# Solution Delivered 
• Developed an interactive dashboard using transaction and customer data from a SQL database, to provide real-time insights.
• Streamlined data processing & analysis to monitor key performance metrics and trends.
• Shared actionable insights with stakeholders based on dashboard findings to support decision-making processes.

# DAX Queries

  1) AgeGroup = SWITCH(
   TRUE(),
   'public cust_detail'[customer_age] < 30, "20-30",
   'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
   'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
   'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
   'public cust_detail'[customer_age] >= 60, "60+",
   "unknown"
   )
  
  
  2) IncomeGroup = SWITCH(
   TRUE(),
   'public cust_detail'[income] < 35000, "Low",
   'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
   'public cust_detail'[income] >= 70000, "High",
   "unknown"
  )

  3) week_num2 = WEEKNUM('public cc_detail'[week_start_date])
  4) Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
  5) Current_week_Reveneue = 
                            CALCULATE(
                                       SUM('public cc_detail'[Revenue]),
                                       FILTER(
                                       ALL('public cc_detail'),
                                       'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])))
  
  6) Previous_week_Reveneue =
                             CALCULATE(
                                         SUM('public cc_detail'[Revenue]),
                                         FILTER(
                                         ALL('public cc_detail'),
                                         'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1))
