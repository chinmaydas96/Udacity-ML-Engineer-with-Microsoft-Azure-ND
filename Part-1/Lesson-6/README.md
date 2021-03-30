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










