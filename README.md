
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


## 1st Temp Table (#CleanedData)

```
with a as
(
select *,
	ROW_NUMBER() over (partition by customer_id, item_id, quantity order by datecreated)dup_flag,
	ROW_NUMBER() over (partition by customer_id order by datecreated) as count_data
	from ecom
	where grand_total > 0
) select *
into #CleanedData
from a 
where dup_flag = 1
```

 ![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/97b42611-3e0d-473f-b87e-1b834cd01057)

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/eb2f3f35-76a0-4f38-b388-95c12c67a068)


## 2nd Temp Table (#Retention)
See the first transaction of each Customer_id and see the cohort date as per transaction

```
select customer_id,
		min(datecreated) as FirstTransaction,
		DATEFROMPARTS(year(min(datecreated)), MONTH(min(datecreated)), 1) as CohortDate
into #Retention
from #CleanedData
group by Customer_Id
```

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/f8f99645-48a2-426f-a1f6-1e50358e09e1)

 ![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/f7cf20c3-8f8f-4156-b8f5-f839c6f1ac88)


## 3rd Temp Table ( #Cohort_Index )
Make the Cohort Index to see the age Transaction of each Customer_id by joining the #CleanedData table and #Retention Table on Customer_id 

```

select a.*,
(invoice_year - cohort_year) * 12 + (invoice_month - cohort_month) +1 as cohort_index
into #Cohort_Index 
from
	(
	select c.*,
			cohortdate,
			YEAR(DateCreated) as invoice_year,
			MONTH(DateCreated) as invoice_month,
			YEAR(cohortdate) as cohort_year,
			MONTH(cohortdate) as cohort_month
		from #CleanedData c
		left join #Retention r
			on c.customer_id = r.customer_id
		) a
  ```
  
![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/06059e6d-cff8-4272-823d-e09bc81c79b3)

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/faff6a83-52e1-458e-8e4b-ca74b29cbb2c)


## Counting the Cohort Index
All of the Temp table needed for analysis is done and now I will be counting the index to see how many indexes there are
 
```
select distinct 
	cohort_index
from #Cohort_Index
```

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/282f5113-6310-4fa0-9f94-b61fa36a9790)
![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/eae048a2-7b59-4b9b-a2de-c5711977d063)


## 4th Temp Table ( #Cohort_Pivot )
I need this Pivot Query to make a final cohort analysis. 
As we see from the index count above, I have 5 indexes, hence why I will be using those 5 in this query. 

```
select *
into #cohort_pivot
from
	(
	select distinct
			Customer_Id,
			CohortDate,
			cohort_index
	from #Cohort_Index
	) tbl
 pivot
 (
	count(Customer_Id)
	for cohort_index in 
	([1],[2],[3],[4],[5])
) as pivottable
order by CohortDate
```

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/6bd8b70d-3a40-4c0c-b1a0-faef0881cf2b)

## Query for Final Cohort Analysis

```
select *
from #cohort_pivot
order by CohortDate
```

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/cd772a38-4b73-4c69-ae25-1f24cb17c5c5)

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/751d975a-f5a4-4726-9445-533ed8bca1d1)

## Percentage Query
 
```
select  
		1.0*[1]/[1]*100 as [1], 
		1.0*[2]/[1]*100 as [2],
		1.0*[3]/[1]*100 as [3],
		1.0*[4]/[1]*100 as [4],
		1.0*[5]/[1]*100 as [5]
from #cohort_pivot
order by CohortDate
```

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/f799b85a-50d0-4031-a787-9d3c047e2bd6)

 ![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/a2d5a8a3-e7c0-4619-abe0-4560da1eb084)


## Tableau Visualization 
If I want to visualize in Tableau. I will be using select distict like this query

```
select distinct
		customer_id,
		CohortDate,
		cohort_index,
		count_data
from #Cohort_Index
order by count_data
```

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/7348df06-361f-4504-81f8-68dacf82c9ad)

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/91a0ea36-e3eb-4d00-8a71-bf59f7abb97b)

## Final Tableau Result

![image](https://github.com/DenidyaFadiya/CohortAnalysis/assets/129844542/21e98eb6-5466-41e9-a1da-dfdf36e0463f)

 

 
