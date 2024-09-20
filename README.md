Project: AWS Lambda EC2 Automation

This project consists of AWS Lambda functions that automate the management of EC2 instances and EBS volumes based on specific criteria (tags, instance states, volume types). The automation scripts handle tasks like starting and stopping EC2 instances in specified AWS regions, as well as modifying Elastic Block Store (EBS) volumes. The project uses Python with the Boto3 library to interact with AWS services.

                      +-------------------------------------+
                      |           AWS Lambda                |
                      +-------------------------------------+
                                   |
                                   |
              +-------------------------+-------------------------+
              |                          |                         |
+-------------------------+  +-------------------------+  +-------------------------+
|   Start EC2 Instances    |  |   Stop EC2 Instances    |  |   Modify EBS Volumes    |
+-------------------------+  +-------------------------+  +-------------------------+
              |                          |                         |
      +-----------------------+   +-----------------------+    +-----------------------+
      |   EC2 Instances (AWS)  |   |   EC2 Instances (AWS) |    |   EBS Volumes (AWS)   |
      +-----------------------+   +-----------------------+    +-----------------------+
                                   |                          |
                                   +--------------------------+
                                           |
                                           |
                               +---------------------------+
                               |    AWS CloudWatch Events   |
                               +---------------------------+
                               |    (Scheduled Automation)  |
                               +---------------------------+


Features:
Start EC2 Instances:
A Lambda function that starts all stopped EC2 instances in a specific AWS region based on custom tags. The region, tag key, and tag value are configured via environment variables.

Stop EC2 Instances:
A Lambda function that stops all running EC2 instances in a specific AWS region, filtered by tags. The function ensures that only tagged instances are stopped and returns a summary of the action.

Modify EBS Volume Types:
A Lambda function that retrieves all available Elastic Block Store (EBS) volumes and modifies their type from gp2 to gp3. This function automates cost optimization by converting legacy volume types to more efficient and cost-effective alternatives.

Technologies Used:
AWS Lambda: Serverless execution of the functions.
Boto3 (AWS SDK for Python): To interact with AWS services like EC2 and EBS.
Python: The scripting language used for automation.
Environment Variables: For dynamic configuration of regions and tags without hardcoding.
Execution Details:
The EC2 instance management functions start and stop instances based on specific environment tags (environment=development) to control which instances are managed by the Lambda function.
The EBS volume management function automatically converts volumes of type gp2 to gp3 for better performance and cost efficiency.
A cron expression (0/10 * * * ? *) can be used to schedule periodic execution of the functions (every 10 minutes in this case).
How to Use:
Set up environment variables (REGION, TAG_KEY, TAG_VALUE) for your Lambda function in the AWS Lambda console.
Deploy the functions via AWS Lambda and schedule them using CloudWatch Events if periodic execution is required.
For local testing, the code can be tested on your MacBook by configuring AWS credentials and using the AWS CLI or by setting appropriate environment variables.
This project simplifies the process of managing cloud resources and optimizing storage costs using AWS services.

