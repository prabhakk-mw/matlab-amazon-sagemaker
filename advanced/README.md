# Run MATLAB Code From Amazon SageMaker Using Hyperparameter Tuning jobs

This tutorial tells you how to run MATLAB code inside the [Amazon SageMaker](https://aws.amazon.com/sagemaker/) environment using Hyperparameter tuning jobs. The tutorial provides example Jupyter notebook that you can use in SageMaker to run a deep learning example, and modify it for your own appplications.

For example, if you trained a network similar to `training.ipynb` notebook, but want to squeeze the last percentange of accuracy, you can experiment with the hyperparamters for your model. Identifying the optimal hyperparemters is a repetitive trial and error process. The idea is to code, experiment, evaluate the outcome, and make changes and repeat the process until you get satisfactory results. The [HyperparameterTuner](https://sagemaker.readthedocs.io/en/stable/api/training/tuner.html) API allows you to automate this process by creating parallel tuning job to get the optimal hyperparameters.

The example Jupyter notebook runs parallel Hyperparameter tuning jobs using Amazon EC2 Spot instances. Managed spot training can optimize the cost of training models up to 90% over on-demand instances. For more information, see [How Hyperparameter Tuning Works
 in SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/automatic-model-tuning-how-it-works.html).

This tutorial builds upon the previous `training.ipynb` notebook, and optimises for the best hyperparameter for our application.

## Launch a SageMaker instance

To launch a SageMaker notebook instance, open the [SageMaker console](https://console.aws.amazon.com/sagemaker/home?region=us-east-1#/notebook-instances) and select notebook instances.

Before launching the instance, go to Additional Configurations and increase the volume size of the notebook from default value of 5 GB to 50 GB.

Note that the IAM role that you select for the notebook must have permission to read from [Amazon S3 buckets](https://s3.console.aws.amazon.com/s3/home) and read/write to [Amazon ECR repositories](https://console.aws.amazon.com/ecr/repositories). For information on setting IAM roles, see the Amazon documentation [here](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Integrating.Authorizing.IAM.S3CreatePolicy.html) and [here](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-policy-examples.html).

Leave everything else at the default values.

## Upload and Run Example Jupyter notebook

To launch a Jupyter notebook server inside the SageMaker instance, go to "Notebook instance" in the SageMaker console, and click the action "Open Jupyter". You can then click the "Upload" button to upload the example notebooks included with this tutorial.
Open the notebook and follow all the steps in it. Run section by section to understand the steps.

## Run MATLAB in SageMaker

After you complete the steps in the example notebooks, you can see how the MATLAB code is called from the notebook. You can also go to ["Hyperparamter tuning jobs"](https://console.aws.amazon.com/sagemaker/home?#/hyper-tuning-jobs) section to see your best tuning job, cost saved, etc.

## Clean up

To avoid incurring unnecessary charges, use the AWS Management Console to delete the resources that you created while running the example -

- Open the Amazon S3 console at https://console.aws.amazon.com/s3/, and then delete the bucket that you created for storing model artifacts and the training dataset.
  
- Open the Amazon ECR console at https://console.aws.amazon.com/ecr/, and then delete the repository that you created for storing MATLAB docker image container.
  
- Open the SageMaker console at https://console.aws.amazon.com/sagemaker/home?#/notebook-instances, and then delete the notebook instance.
  