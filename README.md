Run MATLAB with Amazon SageMaker Using an Example Jupyter Notebook
------------------------

This blog tells you how to run MATLAB code inside the [Amazon SageMaker](https://aws.amazon.com/sagemaker/) environment.  The blog provides an example Jupyter notebook that you can use in SageMaker to run a deep learning example, and modify it for your own appplications.
This is especially helpful for machine learning, deep learning & computer vision workflows which can require high processing power, that you can easily get with cloud solutions.

For example, if you have written MATLAB scripts for training & validation on your data set, but you see your local system is not powerful enough to run these extensive deep learning pipelines, then a solution is to scale up to the cloud. This blog can help you learn how to take an existing deep learning solution and run it on the cloud using Amazon SageMaker. You do not have to spend time configuring your EC2 instances, because you you can directly launch a Jupyter notebook in SageMaker, and run MATLAB code via Processing jobs in SageMaker. You can also change the instance type of each processing job depending on your task. 

This blog shows you how to take [this example](https://www.mathworks.com/help/deeplearning/ug/create-simple-deep-learning-network-for-classification.html) from the Deep Learning Toolbox in MATLAB, and run this code on SageMaker using a Processing job. The example creates a simple deep learning network for classification on an image dataset.


Launch a SageMaker instance: 
--------------------------------

To launch a SageMaker notebook instance, open the [SageMaker console](https://console.aws.amazon.com/sagemaker/home?region=us-east-1#/notebook-instances) and select notebook instances. 

Before launching the instance, go to Additional Configurations and increase the volume size of the notebook from default value of 5 GB to 25 GB. 

Note that the IAM role that you select for the notebook must have permission to read from [Amazon S3 buckets](https://s3.console.aws.amazon.com/s3/home) and read/write to [Amazon ECR repositories](https://console.aws.amazon.com/ecr/repositories). For information on setting IAM roles, see the Amazon documentation [here](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Integrating.Authorizing.IAM.S3CreatePolicy.html) and [here](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-policy-examples.html). 

Leave everything else at the default values. 

Upload and Run Example Jupyter notebook 
--------------------------

To launch a Jupyter notebook server inside the SageMaker instance, go to "Notebook instance" in the SageMaker console, and click the action "Open Jupyter". You can then click the "Upload" button to upload the example notebook included with this blog, which is called `matlab.ipynb`. 

Run MATLAB via Processing Job
----------------------------------

```python
processor = Processor(
    image_uri = processing_repository_uri,
    ...
)
```

This `processing_repository_uri`  is the URI of our docker image which we generated in the notebook and uploaded to ECR. 

```bash
FROM mathworks/matlab-deep-learning
USER root
CMD ["matlab", "-batch", "cd /opt/ml/processing/src_files; main; exit"]
```

 In our Dockerfile, we changed the `CMD` to run the script located at `/opt/ml/processing/src_file` location. 

```python
processor.run(
    inputs=
    [ProcessingInput(
        source="/home/ec2-user/SageMaker/main.m",
        destination="/opt/ml/processing/src_files/"),
    outputs = [
        ProcessingOutput(
            output_name="results",
            source="/opt/ml/processing/output_data",
        ),
    ]
)
```

Finally, in our `processor.run()` command, we mount our local `main.m` to CMD location of the Dockerfile so this scipt is run inside the processing job. 

  

To summarize: The processing job essentially runs a script  `main.m`  which is mounted to every docker container when it starts. 

  

![](https://sagemaker.readthedocs.io/en/stable/_images/amazon_sagemaker_processing_image1.png)
