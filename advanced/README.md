# Run MATLAB Code From Amazon SageMaker as Hyperparameter Tuning jobs

This tutorial showcases the usage of MATLAB code inside the [Amazon SageMaker](https://aws.amazon.com/sagemaker/) environment using Hyperparameter tuning jobs.

## Background

Identifying the optimal hyperparemters is a repetitive trial and error process. The idea is to code, experiment, evaluate the outcome, and make changes and repeat the process until you get satisfactory results. The [HyperparameterTuner](https://sagemaker.readthedocs.io/en/stable/api/training/tuner.html) API allows you to automate this process by creating parallel tuning job to get the optimal hyperparameters.

## Description

This tutorial continues from the  `training.ipynb` notebook and showcases the usage of parallel Hyperparameter tuning jobs allowing you to squeeze the last percentange of accuracy by experimenting with the hyperparamters for your model. For more information, see [How Hyperparameter Tuning Works
 in SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/automatic-model-tuning-how-it-works.html).

 **Note:**  Refer to [`Setup`]() and [`Clean up`]() sections in the original README to know how to best use this respository.
