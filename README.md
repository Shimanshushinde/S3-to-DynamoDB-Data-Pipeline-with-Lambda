# Amazon S3 to DynamoDB Data Pipeline with Lambda.
This guide is to create a project where data from an S3 bucket triggers a Lambda function to copy information into DynamoDB.

# Architecture of the Project

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
