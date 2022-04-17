# Run MATLAB Code From Amazon SageMaker Using Jupyter Notebook

This tutorial showcases the usage of MATLAB code inside the [Amazon SageMaker](https://aws.amazon.com/sagemaker/) environment.

## :books: Background

[Amazon SageMaker](https://aws.amazon.com/sagemaker/) is a fully managed service for data science and machine learning (ML) workflows.
You can use Amazon SageMaker to simplify the process of building, training, and deploying ML models.

## Description

This tutorial showcases the usage of SageMaker using Processing and Training jobs with [this example](https://www.mathworks.com/help/deeplearning/ug/create-simple-deep-learning-network-for-classification.html) from the Deep Learning Toolbox in MATLAB.
The example creates a simple deep learning network for classification on an image dataset.

**Note:**  In this example, MATLAB processes the data in [batch mode](https://www.mathworks.com/help/matlab/matlab_env/commonly-used-startup-options.html), and does not bring up the interactive MATLAB desktop environment.

## :hammer_and_wrench: Setup

### :computer: Launch a SageMaker instance

To launch a SageMaker notebook instance, open the [SageMaker console](https://console.aws.amazon.com/sagemaker/home?region=us-east-1#/notebook-instances) and select notebook instances.

Before launching the instance, go to Additional Configurations and increase the volume size of the notebook from default value of 5 GB to 50 GB.

Note that the IAM role that you select for the notebook must have permission to read from [Amazon S3 buckets](https://s3.console.aws.amazon.com/s3/home) and read/write to [Amazon ECR repositories](https://console.aws.amazon.com/ecr/repositories). For information on setting IAM roles, see the Amazon documentation [here](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Integrating.Authorizing.IAM.S3CreatePolicy.html) and [here](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-policy-examples.html).

Leave everything else at their default values.

### :notebook: Notebooks in this tutorial

The following notebooks showcase the usage of MATLAB from SageMaker.
There are 4 different notebooks included with this tutorial.

| Notebook Name | Description |
|---|---|
|[setup.ipynb](./setup.ipynb) | Creates MATLAB docker image and publishes it to Amazon ECR. Used in all other notebooks here.|
|[processing.ipynb](./processing.ipynb) | Trains a deep learning network via [processing jobs](https://docs.aws.amazon.com/sagemaker/latest/dg/processing-job.html). |
|[training.ipynb](./training.ipynb) | Trains a deep learning network via [training jobs](https://docs.aws.amazon.com/sagemaker/latest/dg/adapt-training-container.html) using spot training to save cost. Using [Managed spot](https://docs.aws.amazon.com/sagemaker/latest/dg/model-managed-spot-training.html) instances for training can optimize costs by upto 90% over on-demand instances.|
|[advanced/tuning.ipynb](./advanced/tuning.ipynb) | Showcases the use of [Parallel Hyperparameter Tuning Jobs](https://docs.aws.amazon.com/sagemaker/latest/dg/automatic-model-tuning-how-it-works.html) with MATLAB.|

### :cloud: Upload and Run Jupyter notebook

* To launch a Jupyter notebook server inside the SageMaker instance:
  * Go to `Notebook instance` in the SageMaker console,
  * Click the action `Open Jupyter`.
  * Click the `Upload` button to upload the example notebooks included with this tutorial.

* Open the notebook and follow all the steps in it. 
* Run section by section to understand the steps.

## :moneybag: Clean up

To avoid incurring unexpected charges, use the AWS Management Console to delete the resources that you created while running the example:

* Open the [Amazon S3 console](https://console.aws.amazon.com/s3/) and then delete the bucket that you created for storing model artifacts and the training dataset.
  
* Open the [Amazon ECR console](https://console.aws.amazon.com/ecr/) and then delete the repository that you created for storing MATLAB docker image container.
  
* Open the [SageMaker console](https://console.aws.amazon.com/sagemaker/home?#/notebook-instances) and then delete the notebook instance.

## Additional resources

* [Amazon SageMaker Examples](https://github.com/aws/amazon-sagemaker-examples)
