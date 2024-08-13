## Central Bank of Liberia's Gender and Department Staff Analysis
### Project Overview
The data provides an overview of the gender distribution and staffing across various departments within an organization. It includes:
- Total staff count: 368 employees.
- Overall gender distribution: 61.96% male and 38.04% female.
- Departmental breakdown: 18 departments with varying gender distributions.
- Key visualizations: A line graph showing the number of male and female staff per department and a table detailing gender distribution percentages for each department.

### Tools
- Python: Used for scripting and extracting data from the CBL annual report.
- Excel: Utilized for cleaning and organizing the extracted data.
- Power BI: Used to build interactive dashboards and final report.
  
### Data Cleaning/Preparation
1. Load and inspect data
2. Standardize column names and department titles
3. Validate gender entries (Male/Female only)
4. Check for and handle missing values
5. Remove any duplicate entries
6. Ensure consistent data types (numbers for counts, text for names)
7. Use pivot tables for initial data summary and anomaly detection
8. Verify totals and percentages for accuracy
9. Export cleaned data for Power BI visualization

### Exploratory Data Analysis
EDA involved exploring the employees data to answer key question, such as:

1. What is the overall gender distribution of the staff in the organization?
  ```
    SELECT 
      gender, 
      COUNT(*) AS staff_count
    FROM 
      CBL_staff_per_gender
    GROUP BY 
      gender;
  ```
2. Which department has the highest gender imbalance?
  ```
    SELECT 
      department, 
      ABS(SUM(CASE WHEN gender = 'Male' THEN 1 ELSE 0 END) - SUM(CASE WHEN gender = 'Female' THEN 1 ELSE 0 END)) AS gender_imbalance
    FROM 
      CBL_staff_per_gender
    GROUP BY 
      department
    ORDER BY 
      gender_imbalance DESC;
```

3. How many departments are there in the organization, and what is the total staff count?

```
    SELECT 
        COUNT(DISTINCT department) AS total_departments, 
        COUNT(*) AS total_staff
    FROM 
        CBL_staff_per_gender;
```

4. What is the trend of male and female staff numbers across different departments?

```
  SELECT 
      department, 
      gender, 
      COUNT(*) AS staff_count
  FROM 
      CBL_staff_per_gender
  GROUP BY 
      department, 
      gender
  ORDER BY 
      department, 
      gender;
````

5. Which departments have the highest and lowest total staff counts?

```
  SELECT 
      department, 
      COUNT(*) AS staff_count
  FROM 
      CBL_staff_per_gender
  GROUP BY 
      department
  ORDER BY 
      staff_count DESC;
  
  SELECT 
      department, 
      COUNT(*) AS staff_count
  FROM 
      CBL_staff_per_gender
  GROUP BY 
      department
  ORDER BY 
      staff_count ASC;
```

### Results/findings

The report reveals that CBL has a total of 368 staff members, with 61.96% males and 38.04% females. The gender distribution varies significantly across departments, with some, like Human Resource Management and Legal, showing a higher proportion of female staff, while others, such as Banking and Financial Markets, are male-dominated. Overall, there is a noticeable gender imbalance across the departments.

### Recommendation
Central Bank of Liberia should:
- Implement recruitment strategies to improve gender balance in male-dominated departments like Banking and Financial Markets.
- Enhance career development for female staff in underrepresented areas to boost leadership.
- Regularly monitor gender distribution to ensure ongoing equity across departments.
