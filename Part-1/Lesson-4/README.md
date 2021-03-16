![1](screen1.png)


---


# Lesson Outline: Training models in Azure

* This lesson is all about training models. Here's what we'll be covering in this lesson:

#### Introduction to Designer : 
First, we'll learn how we can quickly build our models using the no code/low code, drag-and-drop interface of the Designer.

#### Managing pipelines :

We'll cover how to create a pipeline that we manage ourselves using the console, which will allow us to make very small changes that can be run repeatedly. Our goal in managing our pipelines is to do MLOps—that is, to apply a DevOps-based workflow to ML.

#### Running pipelines :

We'll learn how to run pipelines and experiments, as well as how to look at the output and tune our models.

#### Hyperparameters in experiments :

Finally, we'll learn how to use hyperparameters in experiments, including how we can automate the creation of hyperparameters and make very small changes that create huge value in terms of prediction accuracy.

#### Monitoring models with application insights :

Finally, we'll talk about how we can leverage Azure's Application Insights infrastructure to monitor the performance of our models in production.


---

# Introduction to Designer

---

![1](screen2.png)

---

![1](screen3.png)


---

* The Designer is a no code/low code interface that allows you to organize resources using a simple drag-and-drop interface. You can use the Designer to build, test, and deploy your ML models. The Designer can be used to organize and configure a variety of resources, including:

	* Pipelines
	* Datasets
	* Compute resources
	* Registered models
	* Published pipelines
	* Real-time endpoints


---

# Managing Pipelines

---

![1](screen4.png)

---

![1](screen5.png)

---

![1](screen6.png)

---

![1](screen7.png)


## What is Azure Pipelines?

* Azure Pipelines is a cloud service that incorporates the DevOps approach of Continuous Integration (CI) and Continuous Delivery (CD) to automate your ML workflow. With Azure Pipelines, you can:

	* Automatically build and test your code project
	
	* Share your project with others


## Ways to Run Pipelines

* There are several different tools you can use to control a pipeline in Azure:

* You can use the Designer to set up your pipeline using a low code/no code, drag-and-drops interface.

* You can use the console to go through and adjust an existing pipeline.

* You can use the Azure ML SDK to programmatically control your pipeline with Python.

* You can use a notebook to spin up a pipeline, configure it, and rerun it whenever needed.


## Components of an AzureML Pipeline

* An AzureML pipeline has several main components:

#### Data preparation :

This involves steps like importing, validating, cleaning, wrangling (or "munging"), transforming, normalizing, and staging your data. This step tends to be a large proportion of the work in most ML projects.

#### Training configuration :

A typical training configuration includes steps like parameterization, file paths, logging, and reporting.

#### Training validation :

Training validation involves repeatedly running through your experiment, picking different hardware, compute resources, doing distributed computing, and also monitoring your progress.

#### Model deployment :

The final step is to deploy the model. This typically involves actions like versioning, scaling, provisioning, and configuring access control.


## The Azure Machine Learning Workspace

* A lot of the complicated inner workings of a pipeline are automated for you behind the scenes by the Azure Machine Learning Workspace. You can see this in the diagram below:

---

![1](screen8.png)

---


* One key idea to understand is that this system supports an MLOps approach by providing a traceable data lineage—meaning, you have visibility into the process that the data has undergone, including the origin of the data and the root cause of any errors that arise.





















