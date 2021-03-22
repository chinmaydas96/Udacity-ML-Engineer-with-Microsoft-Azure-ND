# Azure ML SDK

---

* This lesson is all about the Azure ML SDK—and in particular, how to use the SDK to programmatically control and automate our machine learning pipelines. 

* Here are the main topics:

	* **Managing data with the SDK :** 

	We'll get into how to manage our cloud resources with the SDK, including how to do monitoring and logging.

	* **Creating pipelines :** 

	We'll talk about how the Azure ML SDK allows us to programmatically explore, create, and manage pipelines. By automating the creation of pipelines 
	We can create much larger numbers of pipelines; also, our pipeline creation becomes a repeatable process that other members of our team can follow.

	* **Managing experiments :** 

	We'll learn how to use the SDK to manage experiments programmatically with Python, allowing us to easily rerun our processes using Python scripts.


---

## The Azure ML SDK

* This lesson is all about the Azure ML Software Development Kit (SDK). The SDK is especially useful to us because it essentially connects two other incredibly useful tools:

	* The Azure ML platform, which gives us the ability to easily automate our machine learning pipelines.

	* The Python ecosystem, which has a rich open source library and allows you to greatly customize your applications.


* The SDK allows you to combine the automation of the Azure ML platform with the customizability of the Python ecosystem to greatly increase the effectiveness, efficiency, and flexibility of your ML applications. Because the SDK is Python-based, it allows us to tap into a rich ecosystem and build a huge variety of tools, from web applications to command-line tools.


---

## Azure ML Key Capabilities

#### Dataset lifecycle : 

You can use the SDK to manage your dataset lifecycle. This includes organizing, monitoring, and logging your ML experiments and resources.

#### Train models : 

The SDK can be used to train a model, either locally or with cloud resources (e.g., to do GPU-accelerated model training).

#### AutoML : 
Using the SDK, you can leverage the power of the cloud platform to automatically iterate through algorithms and hyper parameter tunings to find the best model for running predictions.

#### Web services : 
Finally, you can deploy your web service easily by converting your trained model into a RESTful service that can be consumed by any application.


## Azure ML Modes

#### Stable: 

The stable mode uses an established version to ensure you have a stable environment that you can count on. This is recommended for most use cases.

#### Experimental : 

If you're an early adopter, you can use experimental mode, which is for advanced users who want to try out new features as they become available and are comfortable tolerating some potential bugs.

---

## Managing Data with the SDK

* The Azure ML SDK allows you to automate your machine learning pipeline, and a key part of this automation is using the SDK to manage data. 

* As we've mentioned, the data preparation step in an ML pipeline often makes up a large proportion (not uncommonly about 80%) of the work, so automating the management of this part of the pipeline can make it dramatically more efficient.

* Earlier we mentioned that a dataset can reference data in a Datastore. In addition, a dataset object can also reference a dataset using public web URLs.

## Interfacing with Datasets

* You can interface with Datasets via the API. How you do so depends in part on the type of Dataset you are using. If you recall from an earlier lesson, there are two Dataset types:

#### FileDataset: 

This is a generic Dataset type. This is useful for things like computer vision or anything where you need to have a lot of flexibility.

#### TabularDataset : 

As the name implies, this type is for tabular (i.e., table-based) data. This type allows you to handle formats like JSON, CSV, or Parquet.

* Here's an example of a typical piece of code for interfacing with a FileDataset:

```Python
from azureml.core.dataset import Dataset

url_paths = [
            'http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz',
            'http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz',
            'http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz',
            'http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz'
            ]

dataset = Dataset.File.from_files(path=url_paths)

```	


 * For example we may want to load the data into a Pandas DataFrame, which we can easily do using the to_pandas_dataframe method:

`df = dataset.to_pandas_dataframe()`



















---
![1](screen1.png)