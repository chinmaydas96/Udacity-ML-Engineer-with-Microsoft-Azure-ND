# <center>AutoML and Hyperparameter Tuning</center>

## Outlines 

* In this lesson, we'll see how we can use Automated ML and Hyperparameter tuning to dramatically speed up the development of our models. Here's what we'll be covering:

### Automated ML and SDK : 
We'll discuss how we can use the Azure ML SDK with AutoML to operationalize and automate model creation—allowing you to create models more quickly and accurately.

### Model Interpretation : 
We'll explore how model interpretation allows us to build solutions using AutoML that we (and others) can more easily interpret, making visible the core features that are driving the model.

### Exporting Models with ONNX : 
ONNX is a portability platform for models that was created by Microsoft and that allows you to convert models from one framework to another, or even to deploy models to a device (such as an iOS or Android mobile device).


---

## Hyperparameter Tuning with HyperDrive

* In this section, we'll look at how we can do hyperparameter tuning using HyperDrive.

* Hyperparameters are simply adjustable parameters you choose for model training.

* HyperDrive is a package that helps you automate choosing parameters.


---

## Main Steps for Tuning with HyperDrive

#### Define the parameter search space
	
	* This could be a discrete/categorical variable (e.g., apple, banana, pair) or it can be a continuous value (e.g., a time series value).

#### Define the sampling method over the search space : 
	
	* This is a question of the method you want to use to find the values. For example, you can use a random, grid, or Bayesian search strategy.

#### Specify the primary metric to optimize : 
	
	*For example, the Area Under the Curve (AUC) is a common optimization metric.

#### Define an early termination policy: 

	* An early termination policy specifies that if you have a certain number of failures, HyperDrive will stop looking for the answer.

* Note that to use HyperDrive, you must have a custom-coded machine learning model. Otherwise, HyperDrive won't know what model to optimize the parameters for!

## Controlling HyperDrive with the SDK :

* You can control HyperDrive with the SDK. Here is the example code we looked at in the video:

```python
from azureml.train.hyperdrive import BayesianParameterSampling
from azureml.train.hyperdrive import uniform, choice
param_sampling = BayesianParameterSampling( {
        "learning_rate": uniform(0.05, 0.1),
        "batch_size": choice(16, 32, 64, 128)
    }
)

```

* We also saw that we can specify whether we are tuning a discrete or continuous variable.

* Discrete example:

```python
{
    "batch_size": choice(16, 32, 64, 128)
    "number_of_hidden_layers": choice(range(1,5))
    }
Continuous example:

{    
    "learning_rate": normal(10, 3),
    "keep_probability": uniform(0.05, 0.1)
    }

```

* And finally, we will need to find the best model parameters. Here's an example:

```python
best_run = hyperdrive_run.get_best_run_by_primary_metric()
best_run_metrics = best_run.get_metrics()
parameter_values = best_run.get_details()['runDefinition']['Arguments']

print('Best Run Id: ', best_run.id)
print('\n Accuracy:', best_run_metrics['accuracy'])
print('\n learning rate:',parameter_values[3])
print('\n keep probability:',parameter_values[5])
print('\n batch size:',parameter_values[7])
```

---

## Introducing Automated Machine Learning - 

* In this lesson, we'll get into Automated Machine Learning (which we will sometimes refer to as AutoML). We'll start by first considering some of the issues that come up in traditional machine learning, so that was can then discuss how automated machine learning addresses these issues.

### Traditional ML
To understand why Automated ML is a useful tool, it helps to first understand some of the challenges we face with traditional ML. These include:


#### Focus on technical details vs the business problem : 

* The code and technical details can consume large amounts of the available resources, distracting our focus from the business problem we want to use the ML to solve.

#### Lack of automation : 

* With traditional ML, we have to do many things manually, even though they could easily be automated with tools like Azure ML Studio.


#### Too much HiPPO influence : 

* The Highest Paid Person's Opinion (HiPPO) can have an unduly large influence on decisions about the output of the model, even though this decision might be better made automatically.

#### Feature engineering : 

* What are the features that I need to get the best accuracy? What are the columns I should select? This can be a huge task that requires a lot of human effort.

#### Hyperparameter selection : 

* For example, with a clustering model, what number of clusters will give the best results? There can be a lot of trial and error and many false starts.

#### Training and Tuning : 

* What are the different parameters you're using when training your model? What machines and resources should you use? How should you best tune the parameters? In traditional ML, these questions require a human to supervise the process.

--- 

### Automated ML

* Automated ML can help with all of the above problems. Essentially, AutoML involves the application of DevOps principles to machine learning, in order to automate all aspects of the process. 

* For example, we can automate feature engineering, hyperparameter selection, model training, and tuning. With AutoML, we can:

	* Create hundreds of models a day
	* Get better model accuracy
	* Deploy models faster


* This creates a quicker feedback loop and allows us to bring ideas to market much sooner. Overall, it reduces the time that we have to spend on technical details, allowing for more effort to be put into solving the underlying business problems.


---

# AutoML and the SDK

## Configuring AutoML from the SDK :

* We can easily leverage AutoML from the SDK to automate many aspects of our pipeline, including:

	* Task type

	* Algorithm iterations

	* Accuracy metric to optimize

	* Algorithms to blacklist/whitelist

	* Number of cross-validations

	* Compute targets

	* Training data

* To do this, we first use the AutoMLConfig class. In the code example below, you can see that we are creating an automl_config object and setting many of the parameters listed above:

```python
from azureml.train.automl import AutoMLConfig

automl_config = AutoMLConfig(task="classification",
                             X=your_training_features,
                             y=your_training_labels,
                             iterations=30,
                             iteration_timeout_minutes=5,
                             primary_metric="AUC_weighted",
                             n_cross_validations=5
                            )
```

### Running AutoML from the SDK

* Once we have completed our configuration, we can then run it using the SDK. Here's a typical example of what that would look like:

```python
from azureml.core.experiment import Experiment

experiment = Experiment(ws, "automl_test_experiment")
run = experiment.submit(config=automl_config, show_output=True)
```

---

## Model Interpretation in Azure ML

* The Azure ML platform has some core tools that make it easy to understand model behavior by looking at a previously run experiment. For example, we can easily get visualizations that help us interpret why a model is making the prediction it is making, or identify and select for the best features.

---

## Exporting Models with ONNX

* The Open Neural Network Exchange (ONNX) is an open-sources portability platform for models that allows you to convert models from one framework to another, or even to deploy models to a device (such as an iOS or Android mobile device).

### Getting Models
* To get models with ONNX, there are several options. You can:

	* Train the model in Azure ML
	* Convert an existing model
	* Get a pre-trained ONNX model
	* Create an ONNX model from an AutoML service, such as Azure Custom Vision service


### Using the Runtime

* Installation can be done with a simple pip install, for either CPU or GPU builds:

```
pip install onnxruntime       # CPU build
pip install onnxruntime-gpu   # GPU build
```

* Then we can simply import the runtime and then instantiate an InferenceSession object, passing in the path to the model:

``` Python
import onnxruntime
session = onnxruntime.InferenceSession("path to model")
```

### Practicing with ONNX

* We'll walk through some of the basics of using ONNX. You'll find a notebook below that you can use to follow along and try it for yourself.









































