# Case Study: Analyzing Customer Churn in Power BI

![Dashboard_Overview](https://github.com/ncdas/Analyzing_Customer_Churn_In_PowerBI/blob/4e6e81a9033b55e7364bde627b3454a322c62adf/Dashboard_overview.png "Dashboard_Overview")

# **Project Description**

For subscription-based businesses, reducing customer churn is a top priority. In this Power BI case study, We'll investigate a dataset from an example telecom company called Databel and analyze their churn rates. Analyzing churn doesn’t just mean knowing what the churn rate is: it’s also about figuring out why customers are churning at the rate they are, and how to reduce churn. We'll answer these questions by creating **measures** and **calculated columns**, while simultaneously creating report pages.


# **Exploratory Analysis**
In this step We'll perform Exploratory Analysis. Exploring the new dataset and revisit creating measures in Power BI to get a better understanding of why customers are churning. The following tasks will be performed throughout the exploratory process: 
- Data Check:  
We are checking if there are duplicate rows here. 
To check we created two measures to check if the Count of customers Ids is equal to the count of unique customer Ids.   

        Number of Customers = COUNT('Databel - Data'[Customer ID])

        Number of Unique Customers = DISTINCTCOUNT('Databel - Data'[Customer ID]) 
- Calculating Churn:  
 This is the very first thing we should find out before deep-diving into the analysis. There is a column called `Churn Label` that inidcates "Yes" or "No" but this column isn't easiest to work with.   
 Now we'll convert this column to a binomial column

        Churned = IF('Databel - Data'[Churn Label] = "Yes", 1, 0)  
  indicating if the customer churned or not. Then we'll use that to calculate the churn rate.   

        Churn_rate = DIVIDE([Number of Churned Customers], [Number of Customers]) 

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

# **Investigating Churn Patterns**
In this step 2 I'll investigate all possible churn patterns to find out Why Customers are leaving. 
The tasks wil carried out in this steps are: 
- Analyzing Demographics:  
 In this task we'll analyze the different demographic field from the dataset and create a table to investigate churn pattern. Gather the categorized demographic variables related to age in a new column called `Demographics`
 
        Demographics = IF('Databel - Data'[Senior] = "Yes", "Senior", IF('Databel - Data'[Under 30] = "Yes", "Under 30", "Other"))
We found that the churn rate for senior citizens is 38.46%. which is significantly above average.   

- Age groups(Age Bin):  
As we've seen in that senior citizens churn more often and this suggest that it might be a good idea to analyze the customer age in general. We are going to create age bins and investigate their respective churn rates. We found that as the age increases the average churn rate for age brackets also increases.   

- Inspecting Groups:   
In the task we have analyzed if customers that are part of a group indedd have a lower phone bill, and if it has an impact on the churn rate. And it appears the `Monthly Charge` is significantly lower for peopel who are in  a group of 2 or more. Strengthen this message by adding `Group`.  

- Multiple Fields to Investigate:  
If we look at the metadata info we see there are thre different contract types: "One Year", "Two Year", "Month-to-Month". It would be a good idea to gather the values of yearly contract into one. So we'll have two contract catagory.

        Contract Category = SWITCH('Databel - Data'[Contract Type], "One Year", "Yearly", "Two Year", "Yearly", "Monthly")  
We found that monthly contract churn more that the customers who have yearly based contracts
- Unlimited Plan:   
Databel has a hypothesis that people who are not on an unlimited data are more likely to churn. And it appears that customers who are on an unlimited plan are more likely to churn. Now we'll create anew column called `Grouped Consumption` that classifies the everage monthly GB download. Looks like this:   

        Grouped Consumption = IF('Databel - Data'[Avg Monthly GB Download] < 5, "Light Data User", IF('Databel - Data'[Avg Monthly GB Download] > 10, "Heavy User", "Medium User"))
We found that the churn rate of Light data users who has unlimited plan is the most among others. 
- International Calls:   
In this part of the analysis we'll look into the international activity of customers and its relationship to churn. We discovered that the churn rate for custoemrs who paly for an international plan but don't call internationally is sky high.  

- Advice to Databel:  
 A peice of suggestion for Databel is - "Contact customers who are on an international plan but have not called internationally and propose to downgrade their plan"
