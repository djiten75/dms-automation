
# Introduction
This repository has some sample files that can help create an automated migration of your database using Data migration service from on-prem to AWS. It focues on high level steps that may be required. You will need to customize the steps.

This is not a full implementation but a starting point. It has DUMMY lambda functions that will neeed to be implemented. Some of the steps in the workflow are not going to be needed depending on what your source and target database is.

# Steps
1. Download the project.
2. Create a bucket in your s3 account
3. Upload the parent_step_function.json and child_step_function.json to the bucket.
4. Create the cloudformation stack to create the step function
  aws cloudformation create-stack --stack-name dms_automation --capabilities CAPABILITY_IAM --parameters ParameterKey=s3BucketForStepFunction,ParameterValue=yourbucket --template-body file://./cfn.yml
5.	Run the step function – Go to the console and search for Step function. Find the parent function and select “Run Execution”. 

# Same implementated lambda functions
The project has sample implementation for checking if the DMS Replication instance exists and if not, it will create one. The other steps are stubbed out as being successful. 

Refer to “3. Create Replication Instances (If required)” step in parent_step_function.json and it uses a lambda function to create the instance. The lambda function can be seen in the output of the cloudformation under resource named – CreateDMSRepInstanceFunction
Refer to “4. Check DMS Replication Instance Status” step in parent_step_function.json and it uses a lambda function to create the instance. The lambda function can be seen in the output of the cloudformation under resource named – CheckDMSRepInstanceFunction

These lambda function gives you an idea on how to implement the rest of them for your use case.

# Cleanup
1. Go to AWS Console and select Data Migration Service.
2. Delete the replication instance
3. Delete the stack
  aws cloudformation delete-stack --stack-name dms_automation
