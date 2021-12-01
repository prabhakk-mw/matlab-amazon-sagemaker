What is this blog about?
------------------------

This blog talks about how to run MATLAB code inside the SageMaker environment. This is especially helpful for machine learning, deep learning & computer vision workflows which may require high processing power, easily available via cloud solutions. 

Consider a scenario where you have written MATLAB scripts for training & validation on your dataset - but you see your local system is not powerful enough to run these extensive deep learning pipelines. This is where this blog can help you - we show how to take an existing deep learning solution and run it on cloud using Amazon SageMaker. You do not have to spend time configuring your EC2 instances, you can directly launch a Jupyter notebook via SageMaker and can run MATLAB code via Processing jobs in cloud. You can also change the instance type of each processing job depending on your task. 

In this blog, we take [this example](https://www.mathworks.com/help/deeplearning/ug/create-simple-deep-learning-network-for-classification.html) from Deep Learning toolbox in MATLAB - which create a simple Deep Learning Network for classification on image dataset - and run this on MATLAB SageMaker using Processing job.  


Launching a SageMaker instance: 
--------------------------------

Go to [SageMaker console](https://console.aws.amazon.com/sagemaker/home?region=us-east-1#/notebook-instances) and select notebook instances to launch a SageMaker notebook instance. 

While launching the instance, go to Additional Configurations and increase the volume size of the notebook from default value of 5 GB to 25GB. Note that the IAM role that you select for the notebook should have the permission to read from [Amazon S3 buckets](https://s3.console.aws.amazon.com/s3/home) and read/write to [Amazon ECR repositories](https://console.aws.amazon.com/ecr/repositories). Have a look at [this](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Integrating.Authorizing.IAM.S3CreatePolicy.html) and [this](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-policy-examples.html) documentation from Amazon on how to set the IAM roles. 

Everything else can remain as default values. 

Running Jupyter notebook: 
--------------------------

You can go to "Notebook instance" in the SageMaker console and click "Open Jupyter" action to launch a jupyter notebook server inside the SageMaker instance. You can then click the "Upload" button to upload the notebook shipped along with this blog. 

Running MATLAB via Processing Job:
----------------------------------

```java
processor = Processor(
    image_uri = processing_repository_uri,
    ...
)
```

This is `processing_repository_uri`  is the URI of our docker image which we generated in the notebook and uploaded to ECR. 

```java
FROM mathworks/matlab-deep-learning
USER root
CMD ["matlab", "-batch", "cd /opt/ml/processing/src_files; main; exit"]
```

 In our Dockerfile, we changed the `CMD` to run the script located at `/opt/ml/processing/src_file` location. 

```java
processor.run(
    inputs=
    [ProcessingInput(
        source='/home/ec2-user/SageMaker/main.m',
        destination='/opt/ml/processing/src_files/'),
    outputs = [
        ProcessingOutput(
            output_name="results",
            source="/opt/ml/processing/output_data",
        ),
    ]
)
```

Finally, in our processor.run() command, we mount our local `main.m` to CMD location of the Dockerfile so this scipt is run inside the processing job. 

  

To summarize: The processing job essentially runs a script  `main.m`  which is mounted to every docker container when it starts. 

  

![](https://sagemaker.readthedocs.io/en/stable/_images/amazon_sagemaker_processing_image1.png)
