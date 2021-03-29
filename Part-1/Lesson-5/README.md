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

* To install azureml sdk on local machine.

`pip install pip azureml-sdk -U`

* Check version

```python
import azureml.core
print(azureml.core.VERSION)
```

---

## Create a Virtual Environment and Install IPython

`python -m venv ~/.azure-ml-sdk`
`source ~/.azure-ml-sdk/bin/activate && pip install ipython pip -U`

### Installing and Using the SDK with a Makefile

* One of our main goals in using the Azure ML SDK is to add automation to our Python projects. One way we can do that is to use the SDK is to create an installation step with a Makefile and incorporate the Azure ML SDK with your Continuous Integration workflow.

* A Makefile can include a command to install and upgrade packages in a requirements.txt file. Here's an example in Azure Cloud Shell:

```
(.azure-ml-sdk) udacity@Azure:~/azure-ml-sdk$ cat Makefile
install:
        pip install --upgrade pip &&\
                pip install --upgrade -r requirements.txt
```

The requirements.txt file will look like this:

```
(.azure-ml-sdk) udacity@Azure:~/azure-ml-sdk$ cat requirements.txt
ipython
azureml-sdk
```

* And then, to install, you can simply run `make install` in the shell.

---

## Creating a Pipeline with the SDK


#### Data Preparation

```python
ws = Workspace.from_config() 
blob_store = Datastore(ws, "workspaceblobstore")
compute_target = ws.compute_targets["STANDARD_NC6"]
experiment = Experiment(ws, 'MyExperiment') 

input_data = Dataset.File.from_files(
    DataPath(datastore, '20newsgroups/20news.pkl'))

```

---

#### Training Configuration

```python

output_data = PipelineData("output_data", datastore=blob_store)

input_named = input_data.as_named_input('input')

steps = [ PythonScriptStep(
    script_name="train.py",
    arguments=["--input", input_named.as_download(),
        "--output", output_data],
    inputs=[input_data],
    outputs=[output_data],
    compute_target=compute_target,
    source_directory="myfolder"
) ]

pipeline = Pipeline(workspace=ws, steps=steps)

```

---


#### Training Validation

```python
pipeline_run = experiment.submit(pipeline)
pipeline_run.wait_for_completion()
```


---

## Managing Experiments with the SDK


* Earlier, you learned how to use the Designer to view the results of your previous runs. If we manage our experiments with the SDK, then we can also access this same data—but in a way that gives us greater control and increased functionality. 

* This involves two main tasks: 
	* Listing past experiments  
	* submitting new experiments.

#### 1. Listing Past Experiments

To do this, we need to pass in a workspace object, and then list the collection of trials. This will give us data very similar to the list we've accessed previously using the Designer. Here's the example code we looked at:

```python
from azureml.core.experiment import Experiment

# First, we pass in the workspace object `ws` to the `list` method
# and it returns a Python list of `Experiment` objects.  
list_experiments = Experiment.list(ws)

# If we print the contents of the variable,
# we can see the list of all the experiments
# that have been run in that workspace.
print(list_experiments)

[Experiment(Name: dataset_profile,
 Workspace: Azure-ML-Workspace), Experiment(Name: binary-classification,
 Workspace: Azure-ML-Workspace), Experiment(Name: regression,
 Workspace: Azure-ML-Workspace), Experiment(Name: sfautoml]

```



#### 2. Submitting New Experiments

* To submit a new experiment (such as if we wanted to try a different model type or a different algorithm), we would again pass in a workspace object and then submit the experiment. Here's the example code:

```python
from azureml.core.experiment import Experiment

experiment = Experiment(ws, "automl_test_experiment")
run = experiment.submit(config=automl_config, show_output=True)

```

---


## Edge Cases: SDK Versioning

* One potential issue or "gotcha" that can come up when you're using tools like Jupyter Notebooks or the Azure Cloud Shell is that you may not really know what versions your code is using. Things may run fine for a while and then suddenly stop working because of an issue with the version of one of the libraries being used by your code.


* One way you can address this problem is by pinning your dependencies so that your code always uses a specific known version. For example:

* Jupyter notebooks can do this by using a pip package that has a specific version
Azure Cloud Shell can do this by using a requirements file
For example, here's what that might look like in a requirements.txt file for a Python project:
`
Flask==1.0.2
pandas==0.24.2
scikit-learn==0.20.3
pylint
`

---