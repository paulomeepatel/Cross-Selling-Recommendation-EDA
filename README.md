# Cross-Selling-Recommendation-EDA
Configured & implemented an entire business understanding of banking products of a credit union to increase the cross-selling of products such as current accounts, savings account, credit cards, etc. Analyse the sales data through EDA process and prepared a Tableau Dashboard to dynamically represent corporate the insights and recommended solutions.

## Project Introduction
In this project, our client is a Latin American credit union company XYZ. They are having issues in cross-selling banking products such as credit cards, savings accounts, retirement accounts, and safe deposit boxes. It can take a significant amount of research and business knowledge to increase cross-selling. In order to succeed in the cross-selling area of the business, Data Analyst at ABC analytics is searching for the best technique to be recommended.

## Objective
- The goal of ABC analytics company is to perform Exploratory data analysis on the data provided by the client and gain some meaningful insights. As a Data analyst intern, my job was to perform EDA on the credit union’s dataset and create visualizations to analyze the data and to provide recommendations to the company to increase effective cross-selling of banking products.

## Contents 
- Convert & Load the dataset
- Get an Overview about the data e.g. shape, information and datatypes of the dataset. 
- Data cleaning (if required), check for missing values or delete unwated columns.
- Changing datatypes, making master data.
- Factorizing the data using Pandas
- Data Visualization, show correlation matrix

## Required Packages EDA
- numpy
- pandas
- seaborn
- matplotlib
- datetime

## Importing Packages
```
import numpy as np 
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import datetime
```

## Reading and manipulating data
```
df_raw = pd.read_csv("Train.csv")
```
## Previewing data and datatypes
```
df_raw.head()

fecha_dato	ncodpers	ind_empleado	pais_residencia	sexo	age	fecha_alta	ind_nuevo	antiguedad	indrel	...	ind_hip_fin_ult1	ind_plan_fin_ult1	ind_pres_fin_ult1	ind_reca_fin_ult1	ind_tjcr_fin_ult1	ind_valo_fin_ult1	ind_viv_fin_ult1	ind_nomina_ult1	ind_nom_pens_ult1	ind_recibo_ult1
0	2015-01-28	1375586	N	ES	H	35	2015-01-12	0.0	6	1.0	...	0	0	0	0	0	0	0	0.0	0.0	0
1	2015-01-28	1050611	N	ES	V	23	2012-08-10	0.0	35	1.0	...	0	0	0	0	0	0	0	0.0	0.0	0
2	2015-01-28	1050612	N	ES	V	23	2012-08-10	0.0	35	1.0	...	0	0	0	0	0	0	0	0.0	0.0	0
3	2015-01-28	1050613	N	ES	H	22	2012-08-10	0.0	35	1.0	...	0	0	0	0	0	0	0	0.0	0.0	0
4	2015-01-28	1050614	N	ES	V	23	2012-08-10	0.0	35	1.0	...	0	0	0	0	0	0	0	0.0	0.0	0
5 rows × 48 columns
```
## Renaming Columns
```
#renaming columns

dict = {'fecha_dato' : 'Date',
       'ncodpers' : 'Customer_Code',
       'ind_empleado' : 'Employee_Index',
       'pais_residencia' : 'Country',
       'sexo' : 'Gender',
       'age' : 'Age',
       'fecha_alta' : 'Customer_Join_Date',
       'ind_nuevo' : 'Customer_Index',
       'antiguedad' : 'Customer_Seniority',
       'indrel' : 'Primary_Customer',
       'ult_fec_cli_1t' : 'Customer_Leave_Date',
       'indrel_1mes' : 'Customer_Type',
       'tiprel_1mes' : 'Customer_Relation',
       'indresi' : 'Residence_Index',
       'indext' : 'Foriegner_Index',
       'conyuemp' : 'Spouse_Index',
       'canal_entrada' : 'Channel_Used',
       'indfall' : 'Deceased_Index',
       'tipodom' : 'Primary_Address',
       'cod_prov' : 'Customer_Address',
       'nomprov' : 'Province',
       'ind_actividad_cliente' : 'Activity_Index',
       'renta' : 'Gross_Income',
       'segmento' : 'Segmentation',
       'ind_ahor_fin_ult1' : 'Saving_Account',
        'ind_aval_fin_ult1' : 'Guarantees',
        'ind_cco_fin_ult1' : 'Current_Accounts',
        'ind_cder_fin_ult1' : 'Derivative_Account',
        'ind_cno_fin_ult1' : 'Payroll_Account',
        'ind_ctju_fin_ult1' : 'Junior_Account',
        'ind_ctma_fin_ult1' : 'More_Private_Account',
        'ind_ctop_fin_ult1' : 'Private_Account',
        'ind_ctpp_fin_ult1' : 'Private_Plus_Account',
        'ind_deco_fin_ult1' : 'Short_Term_Deposits',
        'ind_deme_fin_ult1' : 'Medium_Term_Deposits',
        'ind_dela_fin_ult1' : 'Long_Term_Deposits',
        'ind_ecue_fin_ult1' : 'E_Account',
        'ind_fond_fin_ult1' : 'Funds',
        'ind_hip_fin_ult1' : 'Mortgage',
        'ind_plan_fin_ult1' : 'Pensions',
        'ind_pres_fin_ult1' : 'Loans',
        'ind_reca_fin_ult1' : 'Taxes',
        'ind_tjcr_fin_ult1' : 'Credit_Card',
        'ind_valo_fin_ult1' : 'Securities',
        'ind_viv_fin_ult1' : 'Home_Account',
        'ind_nomina_ult1' : 'Payroll',
        'ind_nom_pens_ult1' : 'Pensions2',
        'ind_recibo_ult1' : 'Direct_Debit'
       }

df_raw = df_raw.rename(columns = dict)
```

## datatypes
```
df_raw.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 13647309 entries, 0 to 13647308
Data columns (total 48 columns):
 #   Column                Dtype  
---  ------                -----  
 0   Date                  object 
 1   Customer_Code         int64  
 2   Employee_Index        object 
 3   Country               object 
 4   Gender                object 
 5   Age                   object 
 6   Customer_Join_Date    object 
 7   Customer_Index        float64
 8   Customer_Seniority    object 
 9   Primary_Customer      float64
 10  Customer_Leave_Date   object 
 11  Customer_Type         object 
 12  Customer_Relation     object 
 13  Residence_Index       object 
 14  Foriegner_Index       object 
 15  Spouse_Index          object 
 16  Channel_Used          object 
 17  Deceased_Index        object 
 18  Primary_Address       float64
 19  Customer_Address      float64
 20  Province              object 
 21  Activity_Index        float64
 22  Gross_Income          float64
 23  Segmentation          object 
 24  Saving_Account        int64  
 25  Guarantees            int64  
 26  Current_Accounts      int64  
 27  Derivative_Account    int64  
 28  Payroll_Account       int64  
 29  Junior_Account        int64  
 30  More_Private_Account  int64  
 31  Private_Account       int64  
 32  Private_Plus_Account  int64  
 33  Short_Term_Deposits   int64  
 34  Medium_Term_Deposits  int64  
 35  Long_Term_Deposits    int64  
 36  E_Account             int64  
 37  Funds                 int64  
 38  Mortgage              int64  
 39  Pensions              int64  
 40  Loans                 int64  
 41  Taxes                 int64  
 42  Credit_Card           int64  
 43  Securities            int64  
 44  Home_Account          int64  
 45  Payroll               float64
 46  Pensions2             float64
 47  Direct_Debit          int64  
dtypes: float64(8), int64(23), object(17)
memory usage: 4.9+ GB
```
### Changing datatypes
```
df_raw['Date'] = pd.to_datetime(df_raw['Date'])
df_raw['Customer_Join_Date'] = pd.to_datetime(df_raw['Customer_Join_Date'])
df_raw['Customer_Leave_Date'] = pd.to_datetime(df_raw['Customer_Leave_Date'])

for column in ["Employee_Index", "Country", "Gender"]:
    df[column] = df[column].astype('category')
```

## creating master data
- Keeping just one data for each customer
```
df = df.drop_duplicates(subset='Customer_Code', keep="last")
```

## Visual Insights
- Types of customers
<img src="https://user-images.githubusercontent.com/101534066/196564308-b083cca9-23e3-456c-8e50-a849f5e5de46.png" width="70%" height="70%">
- There are greater number of Inactive Customers than Active Customer.


- Number of Customers by Age
<img src="https://user-images.githubusercontent.com/101534066/196565007-1d8b16f3-5594-4609-80da-ece5e34e5ccd.png" width="70%" height="70%">
- XYZ Credit Unions' the greatest number of customers are in the Adult Age Group.


- Adult age group and Number of Accounts
<img src="https://user-images.githubusercontent.com/101534066/196565256-80ca22da-7536-4767-9f5f-bc1ad058fffc.png" width="70%" height="70%">
- Customers in the age of 40-50 are more likely to possess more than 10 different banking product at XYZ Credit Union.


- Total Number of Different Types of Accounts
<img src="https://user-images.githubusercontent.com/101534066/196565364-22dce395-86a5-423d-82c1-8cb710b758ba.png" width="70%" height="70%">
- The highest number of accounts sold are Current Accounts, Direct Debit, and Private Account; while the lowest sold accounts are Medium Term Deposits, Short Term Deposits, Derivative accounts, Savings Account and Guarantees.

- Number of Customers by Gender
<img src="https://user-images.githubusercontent.com/101534066/196565725-a3c36cea-71d7-40e4-a134-f92bf9c623d3.png" width="50%" height="70%">
- There are more female customers than male customers in XYZ Credit Union.

- Segmentation
<img src="https://user-images.githubusercontent.com/101534066/196565824-9e135a0b-f23c-44dc-a702-f6c644b0cb2e.png" width="50%" height="70%">
- There are approximately 130,000 individuals have accounts with XYZ Credit Union. Nearly 20,000 VIP members are associated with the Union.

- Top 10 channels
<img src="https://user-images.githubusercontent.com/101534066/196565893-96e2ccec-f681-48d6-833a-9854e11213d6.png" width="70%" height="70%">
- Over a million customer have joined XYZ Credit Union through top 10 channels out of total 147 channels.

- Corelation chart
<img src="https://user-images.githubusercontent.com/101534066/196566131-ce529747-e42f-403d-ae17-96ccbffd42d9.png" width="70%" height="70%">
- The above correlation chart shows that Payroll is highly related to Pensions2. And Payroll Account is highly related to Pensions2, Payroll, Debit and Credit Card.

## Basic Insights
- There are more number of Inactive Customers than Active Customer.
- Some accounts are sold together such as Payroll is highly related to Pensions2 and Payroll Account is correlated with Pensions2, Payroll, Debit and Credit Card.
- XYZ Credit Unions's most number of customers are in the Adult Age Group.
- Customers in the age of 40-50 are more likely to possess more than 10 different banking product at XYZ Credit Union.
- The highest number of accounts sold are Current Accounts, Direct Debit, and Private Account; while the lowest sold accounts are Medium Term Deposits, Short Term Deposits, Derivative accounts, Savings Account and Guarantees.
- There are more female customers than male customers in XYZ Credit Union.
- There are approximately 130,000 individuals have accounts with XYZ Credit Union. Nearly 20,000 VIP members are associated with the Union.
- Customers with below average income are more than the customers with above average income.
- The number of individual customers are more than the total number of college graduates and VIPs.
- Over a million customer have joined XYZ Credit Union through top 10 channels out of total 147 channels.

## Recommendations
- Introducing loyalty programs such as health insurance or rewards for engaging with the account may increase the use of accounts that have been inactive for a while (dormant accounts).
- Current account is the most selling banking product in XYZ Credit Union. For the customers having current accunt, scheme of gaining higher interest such as 4.5%, for keeping certain amount in savings account will increase sale of savings account.
- Providing certain benefits to provincial and federal government for projects such as construction, may increase sale of Guarantees.
- Engaging more with adults through social media coverage or advertising will help customers well understand product/services provided by XYZ Credit Union. Direct mail, email, statement inserts, banner ads on website, messages on ATMs, outbound calling campaigns, etc. can be applied as part of customer engagement.
- Engaging more with the top 10 channels used by customers to join the Union will increases chances of getting more customers.
