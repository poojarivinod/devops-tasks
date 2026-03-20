#  Event-Driven Automation using S3, Lambda & CloudWatch 
## Concept Overview 
This setup demonstrates a serverless automation pipeline where an AWS Lambda function is triggered automatically whenever a file is uploaded to an Amazon S3 bucket. 
You don’t have to:   
 Run any code manually   
 Manage or maintain servers   
Everything works automatically in response to events — that’s called Event-Driven Architecture.

## Workflow 
S3 File Upload  →  Lambda Triggered  →  Logs to CloudWatch 

## Tools & Services Involved 
| Service        | Purpose                                                   |
|----------------|-----------------------------------------------------------|
| Amazon S3      | Stores uploaded files and triggers events                 |
| AWS Lambda     | Runs your custom code when triggered                      |
| IAM            | Controls permissions and secure access between services   |
| CloudWatch     | Monitors logs and Lambda executions                       |

## Step-by-Step Implementation 
Step 1: Create a Lambda Function 
1. Go to AWS Console → Lambda → Create function 
2. Choose Author from scratch 
3. Enter function name: 
process_s3_upload 
4. Select Runtime: 
Python 3.11 or Node.js 18 
5. Under Permissions → Change default execution role → Create a new role with basic 
Lambda permissions   
Attach the following IAM policies to the role:   
AWSLambdaBasicExecutionRole → allows CloudWatch logging   
AmazonS3ReadOnlyAccess → allows Lambda to read S3 object details


Configure IAM Roles and Permissions 
A. Lambda Execution Role 
Create an IAM Role for Lambda: 
1. Go to IAM → Roles → Create Role 
2. Select AWS Service → Lambda → Next 
3. Attach: 
o AWSLambdaBasicExecutionRole 
o AmazonS3ReadOnlyAccess 
4. Name it:
lambda-s3-trigger-role 
5. Assign this role to your Lambda under: 
Lambda → Configuration → Permissions 

## Step 2: Add Lambda Code 
Example (Python): 
```
import json

def lambda_handler(event, context):
    print("=== FULL EVENT PAYLOAD ===")
    print(json.dumps(event, indent=2))

    for record in event['Records']:
        bucket = record['s3']['bucket']['name']
        key = record['s3']['object']['key']
        size = record['s3']['object']['size']

        print(f"File uploaded: {key} ({size} bytes) in bucket {bucket}")

    return {"status": "processed"}
```
This code logs all S3 event details to CloudWatch Logs. 

## Step 3: Configure S3 to Trigger the Lambda 
1. Go to S3 → Select your bucket 
2. Click Properties tab 
3. Scroll to Event notifications → Create event notification 
4. Enter name: 
triggerLambdaOnUpload 
5. Under Event types, select: 
All object create events 
6. Under Destination, choose: 
Lambda function →process_s3_upload 
7. Click Save changes 
AWS automatically updates the bucket policy to allow it to invoke your Lambda.

## Step 4: Upload a File to S3 
You can test it manually. 
Option 1 — AWS Console 
1. Go to S3 → Your bucket 
2. Click Upload 
3. Choose a file (e.g., test.txt or image.jpg) 
4. Click Upload   
Option 2 — AWS CLI   
aws s3 cp sample.txt s3://your-bucket-name/   
Once the file uploads, S3 will automatically send a PUT event to trigger your Lambda.  

## Step 5: Verify CloudWatch Logs 
1. Go to AWS Console → CloudWatch 
2. In the sidebar, click Logs → Log groups 
3. Find your log group:   
/aws/lambda/process_s3_upload  

4. Click the latest Log Stream 
You’ll see entries like:   
File uploaded: README.pdf (581836 bytes) in bucket vinod9980  
That confirms your setup is working perfectly.

# Final Architecture Summary

## Architecture Flow

| Step | Component            | Purpose                                      |
|------|---------------------|----------------------------------------------|
| 1    | Lambda Function     | Executes code automatically                  |
| 2    | S3 Trigger (PUT)   | Starts the event when a file is uploaded     |
| 3    | CloudWatch Logs     | Captures execution logs                      |
| 4    | IAM Roles           | Securely connects S3 ↔ Lambda ↔ CloudWatch   |
| 5    | Log Event Payload   | Helps debug and analyze automation           |

## Outcome

Lambda automatically executes after a file is uploaded to S3.


