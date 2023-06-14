# dms-automation
dms-automation

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
