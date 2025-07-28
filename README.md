# ETL-configuration-in-AWS
This project demonstrates the creation of a fully serverless ETL (Extract, Transform, Load) pipeline using AWS services. Raw data stored in Amazon S3 is processed using AWS Glue Studio and queried using Amazon Athena, enabling efficient data analysis without managing any infrastructure.

Goal:
Build a simple ETL pipeline that:
1. Takes raw data from Amazon S3
2. Cleans/transforms it using AWS Glue Studio
3. Saves the processed data back to S3
4. Queries it using AWS Athena

<img width="910" height="118" alt="Screenshot 2025-07-28 at 12 15 33 PM" src="https://github.com/user-attachments/assets/1f6393ea-9ea5-4cd4-b17d-54321b7493da" />

Steps:
1. Create S3 buckets
1 source bucket to upload csv file, 1 target bucket to store the transformed data and 1 bucket to store athena query results.

2. Create IAM role for AWS Glue to access s3 buckets
Go to Rules and choose Glue in service, select s3fullaccess and GlueService Role and click next. Name the role as your wish.

3. Upload customer file in S3 source bucket
Directly uploading file in S3 bucket shows some issue, hence create a folder in S3 and then upload the customer csv file.

4. Set up the Glue Crawler
Go to AWS Glue, under the data catalog in left pane, select Crawler. Crawler is used to crawl out data and show it the console. Create crawler and name it, click next. Add the data source, in our case is S3 and choose S3 path our S3 source bucket, click add on s3 data source, hit next. Choose the IAM role we selected, hit next. Create database name, hit next.

5. Configure Athena
In Glue, click the table and click actions to proceed to Athena query. CLick settings and add the s3 bucket we created to store query results and click save.

6. Create ETL Job
Go to GLue again, click ETL jobs. Under Sources select Amazon S3 and click that icon to modify the S3 source type to Data catalog table, Select Database and Table we created. Now, select Target where we select the target bucket, the file format. Now Under Transforms, search Fields and choose the appropriate parent. Apply the IAM role in job details and hit save.

Now the ETL job will run and save the data in our S3 target bucket.
