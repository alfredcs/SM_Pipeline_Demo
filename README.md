Amazon SageMaker Pipeline Code Sample Demo Instructions

These instructions are intended to cover the process of provisioning a SageMaker Sudio instance and cloning the GitHub repo that is required to run a SageMaker Pipeline demo. This lab does come with a CloudFormation template. 

1.	Click on this [CloudFormation template](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?stackName=cvbootcamp&templateURL=https://aws-workshops-us-east-1.s3.amazonaws.com/cvbootcamp/deployment/cf-sage-maker.yaml) to provision a SageMaker instance with proper permissions.
2.	After the CloudFormation stack has been deployed, click on Output tab and then click URL under Value.
3.	Click Open SageMaker Sudio
4.	Click Commands -> New Terminal to launch a New Terminal
5.	From the newly launched terminal, try: git clone https://github.com/alfredcs/SM_Pipeline_Demo.git
6.	Make the assumed role has needed permission policies to run Sagemaker 
7.	Run different samples using Jupyter Lab or Notebook 
```
		1) sagemaker-pipelines-xgboost-abalone.ipynb: Pipeline demo on regression with Abalone dataset; 
		2) sagemaker-pipelines-customized-project.ipynb: Custimize a pipeline project;  
		3) xgboost_mnist.ipynb: Prediction with a SageMaker build-in algorithm. 
```


CLI Tools:


Available CLI options for SageMaker Pipeline

```
bash-4.2$ aws sagemaker help | grep pipeline
       o create-pipeline
       o delete-pipeline
       o describe-pipeline
       o describe-pipeline-definition-for-execution
       o describe-pipeline-execution
       o list-pipeline-execution-steps
       o list-pipeline-executions
       o list-pipeline-parameters-for-execution
       o list-pipelines
       o send-pipeline-execution-step-failure
       o send-pipeline-execution-step-success
       o start-pipeline-execution
       o stop-pipeline-execution
       o update-pipeline
       o update-pipeline-execution
bash-4.2$ aws sagemaker list-pipelines
{
    "PipelineSummaries": [
        {
            "PipelineArn": "arn:aws:sagemaker:us-west-2:<account-id>:pipeline/abalonepipeline",
            "PipelineName": "AbalonePipeline",
            "PipelineDisplayName": "AbalonePipeline",
            "RoleArn": "arn:aws:iam::<account-id>:role/service-role/AmazonSageMaker-ExecutionRole-20210317T133000",
            "CreationTime": 1632255010.504,
            "LastModifiedTime": 1632260142.207
        }
    ]
}
```

Check for current and previous executions

````
bash-4.2$ aws sagemaker list-pipeline-executions --pipeline-name AbalonePipeline
{
    "PipelineExecutionSummaries": [
        {
            "PipelineExecutionArn": "arn:aws:sagemaker:us-west-2:<account-id>:pipeline/abalonepipeline/execution/4wemqw2sucgh",
            "StartTime": 1632260141.95,
            "PipelineExecutionStatus": "Executing",
            "PipelineExecutionDisplayName": "execution-1632260142207"
        },
        {
            "PipelineExecutionArn": "arn:aws:sagemaker:us-west-2:<account-id>:pipeline/abalonepipeline/execution/sg52s84nu639",
            "StartTime": 1632255076.436,
            "PipelineExecutionStatus": "Succeeded",
            "PipelineExecutionDisplayName": "execution-1632255076521"
        }
    ]
}
```


Check for pipeline execution parameters

```
bash-4.2$ aws sagemaker list-pipeline-parameters-for-execution --pipeline-execution-arn arn:aws:sagemaker:us-west-2:<account-id>:pipeline/abalonepipeline/execution/4wemqw2sucgh
{
    "PipelineParameters": [
        {
            "Name": "ProcessingInstanceType",
            "Value": "ml.p3.2xlarge"
        },
        {
            "Name": "BatchData",
            "Value": "s3://sagemaker-us-west-2-<account-id>/abalone/abalone-dataset-batch"
        },
        {
            "Name": "TrainingInstanceType",
            "Value": "ml.m5.xlarge"
        },
        {
            "Name": "ModelApprovalStatus",
            "Value": "Approved"
        },
        {
            "Name": "InputData",
            "Value": "s3://sagemaker-us-west-2-<account-id>/abalone/abalone-dataset.csv"
        },
        {
            "Name": "ProcessingInstanceCount",
            "Value": "1"
        }
    ]
}
```
