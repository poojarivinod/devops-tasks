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

