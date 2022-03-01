# Run MATLAB Code From Amazon SageMaker Using Example Jupyter Notebook

This tutorial tells you how to run MATLAB code inside the [Amazon SageMaker](https://aws.amazon.com/sagemaker/) environment. The tutorial provides example Jupyter notebooks that you can use in SageMaker to run a deep learning example, and modify it for your own appplications.
This is especially helpful for machine learning, deep learning & computer vision workflows which can require high processing power, that you can easily get with cloud solutions.

For example, if you have written MATLAB scripts for training & validation on your data set, but you see your local system is not powerful enough to run these extensive deep learning pipelines, then a solution is to scale up to the cloud. This tutorial can help you learn how to take an existing deep learning solution and run it on the cloud using Amazon SageMaker. You do not have to spend time configuring your EC2 instances, because you you can directly launch a Jupyter notebook in SageMaker, and run MATLAB code via Processing and Training jobs in SageMaker. You can also change the instance type of each job depending on your task.

The example Jupyter notebook runs training jobs using Amazon EC2 Spot instances. Managed spot training can optimize the cost of training models up to 90% over on-demand instances.

This tutorial shows you how to take [this example](https://www.mathworks.com/help/deeplearning/ug/create-simple-deep-learning-network-for-classification.html) from the Deep Learning Toolbox in MATLAB, and run this code on SageMaker using Processing and Training jobs. The example creates a simple deep learning network for classification on an image dataset. The notebook calls the MATLAB code in batch mode and returns the results. You do not see an interactive MATLAB desktop, just call the code for computation.

## Launch a SageMaker instance

To launch a SageMaker notebook instance, open the [SageMaker console](https://console.aws.amazon.com/sagemaker/home?region=us-east-1#/notebook-instances) and select notebook instances.

Before launching the instance, go to Additional Configurations and increase the volume size of the notebook from default value of 5 GB to 50 GB.

Note that the IAM role that you select for the notebook must have permission to read from [Amazon S3 buckets](https://s3.console.aws.amazon.com/s3/home) and read/write to [Amazon ECR repositories](https://console.aws.amazon.com/ecr/repositories). For information on setting IAM roles, see the Amazon documentation [here](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Integrating.Authorizing.IAM.S3CreatePolicy.html) and [here](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-policy-examples.html).

Leave everything else at the default values.

## Upload and Run Example Jupyter notebook

To launch a Jupyter notebook server inside the SageMaker instance, go to "Notebook instance" in the SageMaker console, and click the action "Open Jupyter". You can then click the "Upload" button to upload the example notebooks included with this tutorial.
Open the notebook and follow all the steps in it. Run section by section to understand the steps.

## Run MATLAB in SageMaker

After you complete the steps in the example notebooks, you can see how the MATLAB code is called from the notebook.

There are 4 different notebooks included with this tutorial.

- `setup.ipynb` - Creates MATLAB docker image and publish it to Amazon ECR.
- `processing.ipynb` - Uses Amazon ECR image, and trains a deep learning network via processing jobs.
- `training.ipynb` - Uses Amazon ECR image, and trains a deep learning network via training jobs using spot training to save cost.

## Clean up

To avoid incurring unnecessary charges, use the AWS Management Console to delete the resources that you created while running the example -

- Open the Amazon S3 console at https://console.aws.amazon.com/s3/, and then delete the bucket that you created for storing model artifacts and the training dataset.
  
- Open the Amazon ECR console at https://console.aws.amazon.com/ecr/, and then delete the repository that you created for storing MATLAB docker image container.
  
- Open the SageMaker console at https://console.aws.amazon.com/sagemaker/home?#/notebook-instances, and then delete the notebook instance.
  