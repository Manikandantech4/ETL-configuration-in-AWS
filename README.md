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
Create S3 buckets
1 source bucket to upload csv file, 1 target bucket to store the transformed data and 1 bucket to store athena query results.

<img width="709" height="181" alt="Screenshot 2025-07-28 at 2 35 10 PM" src="https://github.com/user-attachments/assets/ad513074-32c0-401f-b996-9204fe03b5e0" />


Create IAM role for AWS Glue to access s3 buckets
Go to Rules and choose Glue in service, select s3fullaccess and GlueService Role and click next. Name the role as your wish.

<img width="808" height="181" alt="Screenshot 2025-07-28 at 2 36 35 PM" src="https://github.com/user-attachments/assets/580119db-c380-4f19-ba34-4a05eabce142" />


Upload customer file in S3 source bucket
Directly uploading file in S3 bucket shows some issue, hence create a folder in S3 and then upload the customer csv file.

Set up the Glue Crawler
Go to AWS Glue, under the data catalog in left pane, select Crawler. Crawler is used to crawl out data and show it the console. Create crawler and name it, click next. Add the data source, in our case is S3 and choose S3 path our S3 source bucket, click add on s3 data source, hit next. Choose the IAM role we selected, hit next. Create database name, hit next.

<img width="1109" height="284" alt="Screenshot 2025-07-28 at 2 38 37 PM" src="https://github.com/user-attachments/assets/f20317c2-259b-418f-8851-12a74374fc78" />

Configure Athena
In Glue, click the table and click actions to proceed to Athena query. CLick settings and add the s3 bucket we created to store query results and click save.

<img width="1404" height="667" alt="Screenshot 2025-07-28 at 2 39 49 PM" src="https://github.com/user-attachments/assets/46fa2e01-9ec1-4b6d-8284-9a9af5b8f431" />

Create ETL Job
Go to GLue again, click ETL jobs. Under Sources select Amazon S3 and click that icon to modify the S3 source type to Data catalog table, Select Database and Table we created. Now, select Target where we select the target bucket, the file format. Now Under Transforms, search Fields and choose the appropriate parent. Apply the IAM role in job details and hit save.

<img width="1103" height="516" alt="Screenshot 2025-07-28 at 2 41 38 PM" src="https://github.com/user-attachments/assets/3a143500-299c-4649-a132-132376eb5f5d" />

Now the ETL job will run and save the data in our S3 target bucket.

<img width="1103" height="516" alt="Screenshot 2025-07-28 at 2 41 59 PM" src="https://github.com/user-attachments/assets/d8a32acb-e844-4761-b769-a14ac7f19367" />
