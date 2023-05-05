# Case Study: Analyzing Customer Churn in Power BI

# **Project Description**

For subscription-based businesses, reducing customer churn is a top priority. In this Power BI case study, I'll investigate a dataset from an example telecom company called Databel and analyze their churn rates. Analyzing churn doesn’t just mean knowing what the churn rate is: it’s also about figuring out why customers are churning at the rate they are, and how to reduce churn. I'll answer these questions by creating **measures** and **calculated columns**, while simultaneously creating eye-catching report pages.


# **Step 1: Exploratory Analysis**
In this step I'll perform Exploratory Analysis. Exploring the new dataset and revisit creating measures in Power BI to get a better understanding of why customers are churning. The following tasks will be performed throughout the exploratory process: 
- Data Check:  
We are checking if there are duplicate rows here. 
To check we created two measures to check if the Count of customers Ids is equal to the count of unique customer Ids.   

    `Number of Customers = COUNT('Databel - Data'[Customer ID])`  
    `Number of Unique Customers = DISTINCTCOUNT('Databel - Data'[Customer ID])` 
- Calculating Churn:  
 This is the very first thing we should find out before deep-diving into the analysis. There is a column called `Churn Label` that inidcates "Yes" or "No" but this column isn't easiest to work with.   
 Now we'll convert this column to a binomial column   
  `Churned = IF('Databel - Data'[Churn Label] = "Yes", 1, 0)`  
  indicating if the customer churned or not. Then we'll use that to calculate the churn rate.   
 `Churn_rate = DIVIDE([Number of Churned Customers], [Number of Customers])`  

- Investingating Churn Reason:   
We got the churn rate. Now the next logical step is to investigate the different reason why customer churned. Here's the top 3 churn reason we found:   
    1. Competitior made better offer. 
    2. Competitior had better devices. 
    3. Attitude of support person.   

- Digging Deeper into Churn Categories:  
`Churn Reasons` are grouped together in the `Churn Category` column. The "Extra Data charges", "Price too high" and other price related resons are grouped togather in the "Price" Category. We found the most prevalent churn category is **Competitor**.   

- Use Map.   
The competitors have launched aggressive promos in certain states, and Databel is wondering if it has impacted our customers. Now we are going to use map to find out churn rate by state.   
We found that the most churned state is CA with 63.24% churn rate.   

# **Step 2: Investigating Churn Patterns**
In this step 2 I'll investigate all possible churn patterns to find out Why Customers are leaving. 
The tasks wil carried out in this steps are: 
- Analyzing Demographics. 
- Age groups(Age Bin).
- Inspecting Groups.
- Multiple Fields to Investigate. 
- Unlimited Plan. 
- International Calls. 
- Advice to Databel. 
- Contract Type. 
