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
1. Create S3 buckets:
1 source bucket to upload csv file, 1 target bucket to store and 1 bucket to store athena query results.

2. Create IAM role for AWS Glue to access s3 buckets
Go to Rules and choose Glue in service, select s3fullaccess and GlueService Role and click next. Name the role as your wish.

3. Upload customer file in S3 source bucket:
Directly uploading file in S3 bucket shows some issue, hence create a folder in S3 and then upload the customer csv file.
