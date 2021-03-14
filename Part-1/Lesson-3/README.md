![1](screen1.png)


# Lesson Outline: Datastores and Datasets

* This lesson is all about managing data by using Datastores and Datasets. Here are the main topics we'll cover:

#### Managing data :
	
* We'll talk about some of the MLOps workflows that are enabled by managing data within the Azure ML studio platform.


#### Working with Datasets :
	
* Working with datasets is critical for sharing data and having a high performance pipeline that doesn't require copying the data back and forth.


#### Dataset monitoring and data drift : 

* If you collect your data, train a model, and then you get some new customers, those new customers may not be the correct target for the model that you created previously—you may need to recreate the model to get a better fit. With Dataset monitoring, you can detect those changes.

#### Using Datasets in notebooks : 
	
* We'll cover the workflow for using Datasets in notebook, and we'll show you how you can leverage the open Datasets that are available in Azure.

#### Dealing with sensitive data : 

* One of the most important topics in ML is how to handle personally identifiable information and protect it using encryption.

---


# Managing Data in Azure Machine Learning

![1](screen2.png)

---

![1](screen3.png)

---

![1](screen4.png)


---

# The Problem: Managing Data Without the Cloud

* To understand why we need Datastores—and cloud-based data storage more generally—it helps to first consider the alternative. If you were trying to handle the data on your own local machine, you would be faced with a number of challenges, including:

#### Data governance 

If you have secret or sensitive data that you need to keep protected, data governance becomes a concern.

#### Do-It-Yourself (DIY) interface to data storage types. You will have to write a bunch of extra code to connect different storage types (such as SQL or Databricks).

#### Hardware constraints. Your machine's resources (e.g., CPU, disk IO, storage) are limited.

#### Third party integration. If you want to use an off-the-shelf, third party tool, this could pose integration problems—and you will have to handle the integration problems on your own.

### The Solution: The Azure Cloud and Datastores

Datastores have a number of key properties that address the above challenges:

1. Easy-to-use interface for many storage types. A Datastore is essentially an abstraction that provides easy methods to interact with many different tools and with many different complex data storage types. This removes the extra work of struggling with third-party integrations and writing do-it-yourself interfaces for different data storage types.

2. Secure, centralized control of the data. This means you don't need to have separate systems that move your data to different locations—which results in better efficiency. You don't have to copy the data back and forth; instead, your ML projects can simply use copies derived from that centralized data. This centralized control also includes built-in encryption and thus results in better security.

3. Scalability. Datastores leverage cloud-native elastic storage, meaning that they can scale in response to demand. Obviously, this is something your hard drive cannot do.





































