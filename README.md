# Amazon S3 to DynamoDB Data Pipeline with Lambda.
This project aims to automate the process of triggering an AWS Lambda function upon the arrival of new data in an S3 bucket. The Lambda function is designed to extract relevant information from the newly uploaded data and store it in DynamoDB for further processing and analysis.

# Architecture of the Project
![Untitled Diagram](https://github.com/Shimanshushinde/3-Tier-WebAap-Architecture/assets/137445826/9c0dcfde-233f-48ce-b3b3-2c112ff5ca1d)

## Prerequisites
Before proceeding, ensure the following:

- AWS account with necessary permissions.
- Familiarity with the AWS Management Console.
- Familiarity with AWS Lambda, S3, and DynamoDB.
  
## Steps To Deploy
### Step 1: Create an S3 Bucket
- Go to the AWS Management Console and navigate to the S3 service.
- Create a new bucket or use an existing one to store your data files.

### Step 2: Create a DynamoDB Table
- Navigate to the DynamoDB service in the AWS Management Console.
- Create a new table or use an existing one to store your data.

### Step 3: Create a Lambda Function
- Go to the Lambda service in the AWS Management Console.
- Create a new Lambda function with a trigger from the S3 bucket.
- Write your code to handle the event triggered by the S3 upload. This code will read the file from S3 and write data to DynamoDB.
```sh
import boto3
from uuid import uuid4
def lambda_handler(event, context):
    s3 = boto3.client("s3")
    dynamodb = boto3.resource('dynamodb')
    for record in event['Records']:
        bucket_name = record['s3']['bucket']['name']
        object_key = record['s3']['object']['key']
        size = record['s3']['object'].get('size', -1)
        event_name = record ['eventName']
        event_time = record['eventTime']
        dynamoTable = dynamodb.Table('newtable')
        dynamoTable.put_item(
            Item={'unique': str(uuid4()), 'Bucket': bucket_name, 'Object': object_key,'Size': size, 'Event': event_name, 'EventTime': event_time})

```
### Step 4: IAM Role for Lambda
- Ensure that your Lambda function has permissions to access both S3 and DynamoDB.
- Create an IAM role with policies granting access to S3 and DynamoDB, and attach it to your Lambda function.

### Step 5: Configure S3 Event Trigger
- In the Lambda function configuration, add a trigger from the S3 bucket you created earlier.
- Configure the trigger to listen for events like "ObjectCreated" or "ObjectModified" depending on your use case.

### Step 6: Code Execution
- Write code in your Lambda function to handle the S3 event. This code should:
- Retrieve the object details (e.g., file name, bucket name) from the event.
- Read the data from the S3 object.
- Transform the data if necessary.
- Write the data to the DynamoDB table.

### Step 7: Testing
- Upload a file to your S3 bucket to trigger the Lambda function.
- Monitor the execution in the Lambda console to ensure it completes successfully.
- Check the DynamoDB table to verify that the data has been copied correctly.

### Step 8: Monitoring and Optimization
- Monitor the performance of your Lambda function, S3 bucket, and DynamoDB table.
- Optimize your code and configurations based on usage patterns and performance metrics.
