
# SQL Project - Cohort Analysis Pakistan E-Commerce


![Groceries](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/86e9077a-3945-4e58-8ff2-bbb93821309e)

## This Project I will be analyzing customer retention rate using cohort analysis

Cohort analysis is a behavioral analytics to see the customer behavior that shares the common criteria within a range of time. This analysis is usually used to give the insight on the customer base, to help the users to determine the most suitable market for the product launched. Cohort analysis works by breaking the raw data into related group before analysis. Cohort analysis can be classified into 3 types ; Time-Based, Segment-Based, Size-Based analysis. 
I will be analyzing Time-Based analysis for this Cohort Project Analysis.
In this Cohort Analysis I will be using bunch of Temp Table Functions for easier analysis.

### Checking Duplicate Data
Check any possible duplicate data using dup_flag function, if the dup_flag shows >1 meaning the data is duplicate. Hence why we need to filter the data using dup_flag = ‘1’.

### Count the data with the same Customer_id to see the transactions per Customer_id
From the table each customer’s starts with 1 and every count_data will calculate each time the transactions happened. 
 
 ![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/7705f6c5-024f-4323-bb88-bf3b4ba81049)



## I am going to make temporary table so we don’t have to call the CTE over and over again

## 1st Temp Table (#CleanedData)
 ![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/97b42611-3e0d-473f-b87e-1b834cd01057)

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/eb2f3f35-76a0-4f38-b388-95c12c67a068)

## See the first transaction of each Customer_id and see the cohort date as per transaction

## 2nd Temp Table (#Retention)

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/f8f99645-48a2-426f-a1f6-1e50358e09e1)

 ![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/f7cf20c3-8f8f-4156-b8f5-f839c6f1ac88)


## Make the Cohort Index to see the age Transaction of each Customer_id

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/4b13875a-87b9-4b75-8f47-5db11e0ac6f1)

## 3rd Temp Table ( #Cohort_Index )
 
![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/06059e6d-cff8-4272-823d-e09bc81c79b3)

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/faff6a83-52e1-458e-8e4b-ca74b29cbb2c)

## All of the Temp table needed for analysis is done and now I will be counting the index to see how many indexes there are
 
![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/282f5113-6310-4fa0-9f94-b61fa36a9790)
![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/eae048a2-7b59-4b9b-a2de-c5711977d063)


## Create Cohort Table Analysis
As we see from the index count above, I have 5 indexes, hence why I will be using those 5 in this query. 
![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/0bf89c88-5c3d-4a3f-a14a-737adcea1103)


## 4th Temp Table ( #Cohort_Pivot )
 
![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/6bd8b70d-3a40-4c0c-b1a0-faef0881cf2b)

## Query for Final Cohort Analysis
 
![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/cd772a38-4b73-4c69-ae25-1f24cb17c5c5)

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/751d975a-f5a4-4726-9445-533ed8bca1d1)

## Percentage Query
 
![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/f799b85a-50d0-4031-a787-9d3c047e2bd6)

 ![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/a2d5a8a3-e7c0-4619-abe0-4560da1eb084)


## If I want to visualize in Tableau. I will be using select distict 

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/7348df06-361f-4504-81f8-68dacf82c9ad)

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/91a0ea36-e3eb-4d00-8a71-bf59f7abb97b)

## Final Tableau Result

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/21e98eb6-5466-41e9-a1da-dfdf36e0463f)

 

 
