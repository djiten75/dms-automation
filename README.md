# dms-automation
dms-automation

#Introduction
This repository has some sample files that can help create an automated migration of your database using Data migration service from on-prem to AWS. It focues on high level steps that may be required. You will need to customize the steps.

This is not a full implementation but a starting point. It has DUMMY lambda functions that will neeed to be implemented. Some of the steps in the workflow are not going to be needed depending on what your source and target database is.

#Steps
1. Download the project.
2. Create a bucket in your s3 account
3. Upload the parent_step_function.json and child_step_function.json to the bucket.
4. Create the cloudformation stack to create the step function
  aws cloudformation create-stack --stack-name dms_automation --capabilities CAPABILITY_IAM --parameters ParameterKey=s3BucketForStepFunction,ParameterValue=yourbucket --template-body file://./cfn.yml


#Cleanup
1. Go to AWS Console and select Data Migration Service.
2. Delete the replication instance
3. Delete the stack
  aws cloudformation delete-stack --stack-name dms_automation
