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