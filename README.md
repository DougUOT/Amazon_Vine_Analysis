# Amazon_Vine_Analysis
Analyzed 50 datasets of Amazon reviews written by members of the paid Amazon Vine program. Implemented ETL using Amazon Web Services, PySpark and Postgres SQL.

## Overview of Project

The client $ellby is about to release a large catalog of products on a leading retail website. They want to know how the reviews of their products compare to the reviews of similar products sold by their competitors. They're also interested in enrolling in a program that gives out free products to select reviewers but they want to know if it's worth the cost. There are thousands of reviews and they're in words not numbers so you'll need to translate them in order to analyze them.

In this project, we'll dig into what the industry means by big data. We'll explore the big data ecosystem including Hadoop, the four V's (Volume, Velocity, Variety and Veracity), MapReduce, Google Colaboratory and Spark. We'll also cover natural language processing (NLP). We'll close with an introduction to cloud services. Cloud services let us store large amounts of data at remote locations rather than locally, on top of many other services. This allows for more scalability and performance. We'll use the most popular cloud service available: Amazon Web Services (AWS). 

This assignment is related to the Bootcamp Data Analytics from the University of Toronto. It comprises the goals below for this module: 

Follow below the goals for this module:

1) Objective 1: Perform ETL on Amazon Product Reviews
2) Objective 2: Determine Bias of Vine Reviews


## Resources

* Data Source: [Amazon_Reviews_ETL.ipynb](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb) and [Amazon_Vine_Analysis.ipynb](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Amazon_Vine_Analysis.ipynb). The schema SQL is available on [challenge_schema.sql](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/challenge_schema.sql). Amazon Dataset available on https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt
* Software & Data Tools: Python 3.8.8, Visual Studio Code 1.64.2, PySpark in Google Colab Notebook, Pyspark 3.0.3, AWS RDS-Postgresql and PgAdmin 5.7

## Results & Code

## Objective 1: Perform ETL on Amazon Product Reviews

  * From the following Amazon Review datasets (Links to an external site.), pick a dataset that you would like to analyze.
  
  We selected the videogame Dataset (https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Video_Games_v1_00.tsv.gz)
  
  * Install packages for libraries that we want to use. Running with cloud notebooks with PySpark.
![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab1.PNG)

  * Loading Amazon Data into Spark DataFrame
![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab2.PNG)

  * Creating DataFrames to match tables. Read in the review data set as a Dataframe and creating the customers_table DataFrame.
  * Using the groupby() function on the customer_id column of the DataFrame. Count all the customer ids using the agg() function by chaining it to the groupby() function. After  we use this function, a new column will be created, count(customer_id). Rename the count(customer_id) column using the withColumnRenamed() function so it matches the schema for the customers_table in pgAdmin.
![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab3.PNG)

  * Create the products_Table DataFrame
  * Create the products_table, use the select() function to select the product_id and product_title, then drop duplicates with the drop_duplicates() function to retrieve only unique product_ids
![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab4.PNG)

  * The review_id_table DataFrame
  * To create the review_id_table, use the select() function to select the columns that are in the review_id_table in pgAdmin (as shown in the following image), and convert the review_date column to a date

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab4.PNG)

  * The vine_table DataFrame
  * To create the vine_table, use the select() function to select only the columns that are in the vine_table in pgAdmin

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab5.PNG)

  * Load the DataFrames into pgAdmin
  *  Make the connection to your AWS RDS instance. Load the DataFrames that correspond to tables in pgAdmin. In pgAdmin, run a query to check that the tables have been populated.

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab6.PNG)
![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/PgAdmin.PNG)

  * Customer Table on Pgadmin (SQL)

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Customer_table_Pgadmin.PNG)

  * Product Table on Pgadmin (SQL)

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Product_table_Pgadmin.PNG)

  * Review_ID Table on Pgadmin (SQL)

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Review_ID_table_Pgadmin.PNG)

  * Vine Table on Pgadmin (SQL)
  
![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Vine_table_Pgadmin.PNG)


## Objective 2: Determine Bias of Vine Reviews

  * There is a DataFrame or table for the vine_table data using PySpark method 

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab7_0.PNG)
![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab7.PNG)
![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab8.PNG)

  * The data is filtered to create a DataFrame or table where there are 20 or more total votes

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab9.PNG)

  * The data is filtered to create a DataFrame or table where the percentage of helpful_votes is equal to or greater than 50% 

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab10.PNG)

  * The data is filtered to create a DataFrame or table where there is a Vine review (Paid) 

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab11.PNG)

  * The data is filtered to create a DataFrame or table where there isn’t a Vine review (unpaid)
![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab12.PNG)

  * The total number of reviews, the number of 5-star reviews, and the percentage 5-star reviews are calculated for all Vine and non-Vine reviews

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Code%20Google%20Colab13.PNG)

## Vine Program Overview

### SUMMARY

1) Due to the huge difference in number of reviews between a Vine member and a non-member, we can conclude that there is no strong relationship between the numbers. A more in-depth and detailed analysis would be necessary to obtain a better conclusion.
2) On the other hand, due to the very low number of reviews made by Vine members (94 members), only 48 members gave a 5-star review. The company $ellby may distribute free products to selected reviewers as it is worth the cost.
3) According to the results, just 0.2% (94 members) of the Vine member (Paid) provides a review for videogame products.
4) Still, according to the results, just 0.3% (48 members) of the Vine member (Unpaid) provides a 5-star review for videogame products, it is represent 51.06%.
5) More than 50% of Vine member provided a 5-stars review for videogames products
 

![](https://github.com/DougUOT/Amazon_Vine_Analysis/blob/main/Resources/Images/Vine%20Analysis%20Overview.PNG)

###  RECOMMENDED ADDITIONAL ANALYSIS

1) Develop a new analysis, separated by video game categories, selecting keywords from the main video game consoles, such as PS3, PS4, XBOX, and Nintendo.
2) Include three to five stars from reviews for additional analysis 
3) Add PC game review 
