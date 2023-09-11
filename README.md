# Real-time-API-reference



Using the Environment Agency Real Time Flood Monitoring API
(http://environment.data.gov.uk/flood-monitoring/doc/reference), collect the past 24 hours’ worth of data for each monitoring station. Consider scalability and performance optimisation for handling many monitoring stations and frequent updates.

From the pipeline you implement please answer the following questions:
*Only a few sentences are required for each.

1. Please provide your justification for the technologies used and explain your thought process. I prefer to use python, due to its ease of use and rich ecosystem for data processing with resilient libraries.
   
2. Please explain how you would deploy this solution to the cloud to run on recurrence and to publish the dataset in a way that can be served to other internal applications, Data Analysts and Data Scientists. Azure synapse would also be suitable but I will go for AWS

Data Processing: AWS Lambda for serverless data processing.

Cloud Platform: Amazon Web Services (AWS) due to its scalability, reliability, and wide range of services.

Data Storage: Amazon S3 for storing raw data and Amazon DynamoDB or Amazon Redshift for structured data storage.

Create an AWS Lambda function to fetch data from the API, process it, and store it in S3 or DynamoDB.

Use AWS CloudWatch Events to trigger the Lambda function at regular intervals (e.g., every hour).

Store the data in a well-structured format (e.g., JSON or CSV) in S3 for easy access by stakeholders.

   
3. Should the volume of stations increase by 100 times how would your approach change?

Definately, the design has to change. Use AWS Lambda's built-in scaling capabilities to handle increased load automatically(scaling/loadbalancing). Amazon SQS to manage the queue of monitoring stations if the volume becomes extremely high. In addition, you can create a topic/subscriber with SNS for real-time notification.


4. If there was a requirement to live-stream the data, how would your approach change?

Implement a streaming solution using AWS Kinesis or AWS IoT Core to handle real-time data.

Use AWS Lambda to process and aggregate the streaming data for storage.

Consider using AWS Athena and Glue for real-time data transformation and analysis.

5. How would you implement an update strategy that captures the new reading for each station ensuring there is always a maximum of 24 hours’ worth of data retained for each?

Modify the Lambda function to fetch data at shorter intervals (e.g., every 15 minutes).

Implement data retention policies to automatically delete data older than 24 hours.

Use AWS S3 Object Lifecycle policies or DynamoDB TTL to manage data retention.


6. Please briefly explain how you would implement CI/CD and version control.

Use a version control system like Github or SVN

Implement CI/CD pipelines using AWS CodePipeline, Jenkins, or similar tools.

Automate testing and deployment processes for the Lambda function and infrastructure changes using Terraform or configuration management with Ansible

