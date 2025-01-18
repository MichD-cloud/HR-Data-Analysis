# HR-Data-Analysis

### Project overview
The project aims at analyzing HR data to track key HR metrics to enable the department monitor and manage various aspects of employee data and maintain a healthy work force.

### Tools
 -Power BI
 -Tableau 
 -SQL

### Exploratory Data Analysis
Key Performance Indicators
1.	Employee Count
2.	Attrition Count
3.	Attrition rate
4.	Active Employees
5.	Average Age

Charts 

1.	Attrition by Gender
2.	Department wise attrition
3.	Number of employees by age group
4.	Job satisfaction rating
5.	Education field-wise attrition
6.	Attrition rate by gender for different age groups

<img width="468" alt="BI" src="https://github.com/user-attachments/assets/cab18b6a-fc8f-4513-97b2-434221b7ddd9" />

<img width="699" alt="Tb" src="https://github.com/user-attachments/assets/acadbe0c-2684-4c54-8c9b-9658d3113d93" />

### Data analysis

   Create a dashboard using Power BI
 
   Create a dashboard using Tableau
 
   Data Validation using SQL 

   --test employee count
```sql
select sum(employee_count) as Employee_count
from Hrdata
where education = 'Associates Degree' and department = 'Sales'
```

![Picture3](https://github.com/user-attachments/assets/b08804f3-7813-45a6-8f29-9d7c53962b07)

--test Attrition 
```sql
select count (attrition)as attrition_count
from Hrdata
where attrition = 'Yes' and education = 'High School' and 
Job_role ='Research Director'
```

-- test attrition rate
```sql
select round(((select count (attrition) from Hrdata where attrition = 'Yes'and gender = 'Female') /
sum(Employee_count))*100, 2) as attrition_rate from Hrdata
where gender = 'Female'
```

--test Active Emplyees
```sql
select sum(Employee_count) - (select count (attrition) from Hrdata where attrition = 'Yes' and department = 'R&D') as active_employes
from Hrdata
where department = 'R&D'
```

--avg age
```sql
select round(avg (age),0) 
from Hrdata
where education_field ='Other'
```

--test attrition by gender
```sql
select gender, count(attrition) as attrition_count
from Hrdata
where attrition = 'Yes'
group by gender
order by count(attrition) desc
```

--test department wise attrition 
```sql
select department, count(attrition),
round(cast (count(attrition) as numeric) / ((select count (attrition) from Hrdata where attrition = 'Yes')) * 100,2) as pct
from Hrdata
where attrition = 'Yes'
group by department
```
