# YouTube Analytics Automation

This project automates the process of collecting and analyzing YouTube channel statistics using AWS and Google APIs. It includes a scheduled ETL pipeline to retrieve, process, and store data for reporting and analysis.

## Project Overview

The ETL pipeline uses:

- Google Cloud Console to generate a YouTube Data API key.

- AWS S3 for input and output storage.

- AWS Lambda for running the ETL logic.

- AWS EventBridge to automate scheduled data pulls.

# Prerequisites

    - AWS Account with permissions to manage Lambda, S3, and EventBridge.
    - Google Cloud Console Account with access to YouTube Data API v3.

# Setup Guide

Step 1: Generate YouTube API Key

    Go to the Google Cloud Console.

    Enable YouTube Data API v3 and generate an API key.

    Save the API key for later use in the Lambda function.

Step 2: Create S3 Buckets in AWS

    In AWS, create two S3 buckets:

    bucket_input_stats – to hold the input CSV file with YouTube channel IDs.

    bucket_output_stats – to store the processed output data.

    Upload the channels_to_analize.csv file to bucket_input_stats. (You can add or remove channels from this file as needed.)

Step 3: Set Up AWS Lambda Function

    Go to AWS Lambda and create a new function using Python 3 as the runtime.

    Select Create a new basic role. Then, go to IAM to assign AmazonS3FullAccess policy to this role.

    In the Lambda function, add the AWSSDKPandas-Python39 layer (latest version).

    Add the code from lambda_demo.py to your Lambda function.

    Click Deploy to finalize.

Step 4: Configure and Run a Test

    In Lambda, create a test environment named demo_youtube.

    Run the test. Ensure it executes successfully.

Step 5: Schedule Automation with EventBridge

    Go to Amazon EventBridge and create a new rule named automate_ytb_2.

    Under rule type, choose Schedule.
    
    Click Continue with rule creation and set a schedule expression, such as 59 6 * * ? * to run at 8:00 AM PST on the first Monday of each month.
    
    Click Create rule to finish.
    
    Go back to Lambda and add an EventBridge trigger to automate data pulls.

# Folder Structure

    /lambda_demo.py – Core Lambda function code.
    /channels_to_analize.csv – List of YouTube channels to analyze.
    README.md – Project documentation.

# Usage
    Once configured, this pipeline will automatically retrieve and store YouTube analytics data on a scheduled basis for analysis and reporting.

# Future Enhancements
    Add error handling and logging for better tracking.
    Expand the ETL pipeline to process additional YouTube data metrics.