# AWS-Athena
AWS Athena is a server less interactive querying service provided by AWS that is built on top of PrestoDb. 

## AWS Athena
Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is serverless, so there is no infrastructure to manage, and you pay only for the queries that you run.

In order to use Athena, all we have to do is load data into S3, tell Athena which bucket to look at, define a schema and start querying. It was built with data analytics in mind and it is particularly good for:
- Interactive, ad-hoc querying. For instance, you can use Athena to run one time queries against server logs to troubleshoot reporting discrepancies or performance issues
- Integrating with Jupyter Notebooks (or other notebook based solutions) for data scientists/analysts for building interactive analytical solutions with data.


### Provisioning a Athena Service:
**1. Setting up S3 bucket**
- Because this is your first time using Athena, you will have to create an S3 bucket to hold your athena data.
- Click on the blue banner to open up the settings dialog. 
- Now, in a new tab, open up AWS Console again and type in S3.
- Then, create a folder within this bucket.
- Finally, go back to your Athena tab so that you can fill out the query result location field with the location of the S3 bucket that you just created.
![athena set up](https://user-images.githubusercontent.com/6689256/82136020-1a1b9700-97d7-11ea-8ecc-e43d7f8e3de0.PNG)

**2. Setting up Glue**
- Click on Add tables using a crawler to get started on your first Glue table!
- Specify a reasonable name without any spaces or punctuation before continuing. For crawler type, pick Data stores 
- In the next screen, choose S3 for the data store and point to your S3 bucket “yelp” subfolder (or whatever it is you called it).
- For now, pick No on the Add another data store screen.
- An IAM role is how AWS manages permissioning across services. For our purposes, Create an IAM role so that AWS can automatically apply the correct permissions needed for the Athena and Glue and S3 services to talk to each other.
- In the next screen, click on the Add database button to create a new db for our tables.
- Call your db anything you want, just remember no spaces or punctuation
- After clicking Create, click on the Grouping behavior for S3 data option and choose Create a single schema for each S3 path.
- For the last screen, ensure all of your input data is accurate.
- After hitting the Finish button and creating your crawler, click on the Run Crawler button:
- Click into your crawler to view the table:
- Click into the table to view the schema:
![glue](https://user-images.githubusercontent.com/6689256/82136027-2b64a380-97d7-11ea-8207-0163286321e0.PNG)

**3. Using AWS Athena service**
- Now, go back to the Athena page, select yelp-db (if that is what you called your database on glue) on the top left and write the following, simple query:
```
SELECT state, COUNT (*) as num_states
FROM yelp
GROUP BY state
ORDER BY num_states DESC
LIMIT 10;
```
![athena_query](https://user-images.githubusercontent.com/6689256/82136025-243d9580-97d7-11ea-81cd-7f69d1ac8dae.PNG)
