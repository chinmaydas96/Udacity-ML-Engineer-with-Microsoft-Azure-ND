# Deploy a Model 

---

## Introduction

![](screen1.png)

* In this lesson we will talk about model deployments, and what are all the important details you want to be aware of when shipping models into production.

* Deploying a model is a crucial step towards a robust workflow. To get a model into production, several things need to take place. We will cover these topics in this lesson.

	* Enabling Security and Authentication
	* Configuring Deployment Settings
	* Deploying a Model
	* Troubleshooting
	* Benefits of compute instances


---

## Best Practices of DevOps Professionals

![](screen2.png)

* Some of the most important best-practices of DevOps professionals are introduced in this section. Constant evaluation and monitoring, along with a robust deployment is a good way to survive disruptive changes.


#### DevOps: A set of best practices that helps provide continuous delivery of software at the highest quality with a constant feedback loop.


* Chapter 7 of Python For DevOps has an excellent section about logging and troubleshooting.

---

## Enable Security and Authentication :


* Authentication is crucial for the continuous flow of operations. 

* Continuous Integration and Delivery system (CI/CD) rely on uninterrupted flows. 

* When authentication is not set properly, it requires human interaction and thus, the flow is interrupted. 

* An ideal scenario is that the system doesn't stop waiting for a user to input a password. So whenever possible, it's good to use authentication with automation.

---


![](screen3.png)

---

![](screen4.png)

---

### Authentication types

* Key- based
	* Azure Kubernetes service enabled by default
	* Azure Container Instances service disabled by default

* Token- based

	* Azure Kubernetes service disabled by default
	* Not support Azure Container Instances

* Interactive

	* Used by local deployment and experimentation (e.g. using Jupyter notebook)

---

![](screen5.png)

---

![](screen6.png)

---

### Service Principal

* A “Service Principal” is a user role with controlled permissions to access specific resources. Using a service principal is a great way to allow authentication while reducing the scope of permissions, which enhances security.


#### CI/CD : 
	
	* Continuous Integration and Continuous Delivery platform. Jenkins, CircleCI, and Github Actions are a few examples.

	* Further reading: 
		
		* Both the Jenkins and Github Actions websites have good information about their CI/CD platforms and why they are compelling the CI/CD platform.

		* https://www.jenkins.io/

		* https://github.com/features/actions


---

## Implementing Enable Security and Authentication


* In this demo, the Service Principal gets enabled and the many steps of getting to create one are performed successfully.


* Install azure cli packages in terminal 

`pip install azure-cli `



### Several steps are needed to create the Service Principal: 

![](screen7.png)

* Ensure the az command-line tool is installed along with the ml extension

	* The Azure Machine Learning extension allows you to interact with Azure Machine Learning Studio, part of the az command. Ensure it is installed with the following command: `az extension add -n azure-cli-ml`


* Create the Service Principal with az after login in

	`az ad sp create-for-rbac --sdk-auth --name ml-auth`

* Capture the "objectId" using the clientID:

	`az ad sp show --id xxxxxxxx-3af0-4065-8e14-xxxxxxxxxxxx`

* Assign the role to the new Service Principal for the given Workspace, Resource Group and User objectId

	`az ml workspace share -w Demo -g demo --user xxxxxxxx-cbdb-4cfd-089f-xxxxxxxxxxxx --role owner`

* workspace and group can be found at machine learning studio or at the config.json file.

![](screen9.png)


* Exercise: Create a Service Principal Authentication method
In this exercise, you will create a Service Principal which is a good way to authenticate to Azure ML services.

* Now create the Service Principal (SP). Remember you can use whatever name you want, although in the examples used ml-auth.

* Note: you won't be able to create a Service Principal if you are using the lab provided to you, an error like this ValidationError: Insufficient privileges to complete the operation will appear. It is because you are not authorized to create a Service Principal on the Udaicty account. But this will not be a blocker for other exercises in the course. There should not be any issues if you are using your own account. We still encourage you to follow the demo and type in the command and see the information and output come from Azure.


--- 

## Configure Deployment Settings

* Deployment is about delivering a trained model into production so that it can be consumed by others. Configuring deployment settings means making choices on cluster settings and other types of interaction with a deployment. Having a good grasp on configuring production environments in Azure ML Studio and the Python SDK is the key to get robust deployments.

* ACI and AKS
Both ACI and AKS are available in the Azure ML platform as deployment options for models.

* ACI is a container offering from Azure, which uses container technology to quickly deploy compute instances. The flexibility of ACI is reduced as to what AKS offers, but it is far simpler to use.

* AKS, on the other hand, is a Kubernetes offering. The Kubernetes service is a cluster that can expand and contract given on demand, and it does take more effort than the container instance to configure and setup.

#### New terms

* ACI: Azure Container Instance

* AKS: Azure Kubernetes Service

* Deployment: A way to deliver work into production

* Concurrent Operations: Also referred to as "concurrency", it is the number of operations to run at the same time


---

![](screen10.png)

---


## Deploy an Azure Machine Learning model

* The primary task as a Machine Learning engineer is to ship models into production. Constant evaluation allows identifying potential issues and creating a baseline so that adapting or updating is possible.

![](screen11.png)

* Some key steps to deploy a model are:

	* A previously trained model
	* Complete the deployment form
	* Enable authentication
	* Select or create a new compute cluster

![](screen12.png)	

#### New terms
* Constant Evaluation: A feedback loop that is necessary to detect potential issues


---

## Enable Application Insights

![](screen13.png)	

* We discussed Application Insights that is a very useful tool to detect anomalies, visualize performance. 

* It can be enabled before or after a deployment. 

* To enable Application Insights after a model is deployed, you can use the below command with the python SDK. 

`
# enable application insight
service.update(enable_app_insights=True)
`

![](screen14.png)	

---

#### New terms

* Logging: Informational output produced by the software, usually in the form of text

* Application Insights: A special Azure service which provides key facts about an application

* Webservice: One of the most used Python classes from Azure's Python SDK


#### Further reading

* Azure's documentation has a whole section on monitoring and collecting data with Application Insights

* https://docs.microsoft.com/en-us/azure/machine-learning/how-to-enable-app-insights

---

## Troubleshoot Deployment Issues

* We covered different techniques and diagnosis that you can use to identify potential issues like unhandled exceptions from a deployed service. 

* Using local deployment is a special technique, which makes it easier to identify some of these potential issues.

### Common HTTP errors:

* 502: the application crashes because of an unhandled exception.

* 503: there are large spikes in requests and the system is not able to cope with all of them.

* 504: request timed out.

![](screen15.png)

### Deploy Locally

* To deploy locally using the Python SDK you will need to use the LocalWebService class and configure it for a local deployment

![](screen16.png)

```python
from azureml.core.webservice import LocalWebservice

deployment_config = LocalWebservice.deploy_configuration(port=9001)
# Deploy the service
service = Model.deploy(ws, "local-service", [model], inference_config, deployment_config)
print(service.run(input_data=json_data))


service.reload()
print(service.run(input_data=json_data))
```


* Deploying locally has some benefits. First, it is easier and faster to verify unhandled exceptions from the scoring script since you don't have to wait for deployment in Azure. Also, many people or teams can debug at the same time.

#### New terms

* HTTP Status code: A number that represents a status when an HTTP server responds. Error conditions in the server side start at 500

#### Further reading

* The troubleshoot deployment of models section of Azure's documentation covers some of these troubleshooting concepts in detail.

* https://docs.microsoft.com/en-us/azure/machine-learning/how-to-troubleshoot-deployment

## Troubleshoot Deployment Issues

* There are multiple things you can expect to go wrong. When you submit HTTP requests to a deployed model, there are three HTTP codes that you may encounter:

	* HTTP STATUS 502: After a deployment, the application crashes because of an unhandled exception.

	* HTTP STATUS 503: When there are large spikes in requests, the system may not be able to cope with all of them and some clients may see this code.

	* HTTP STATUS 504: The request timed out. In Azure, the requests time out after 1 minute. If the score.py script is taking longer than a minute, this error code will be produced.

* When an error code shows up, one thing you can do is retrieving the logs output. Logs output is always useful to debug problems in deployed containers. Showing below is an extract of what you should see in a successful response to a scoring request.

```
Validation Request Content-Type
Received input: {'data': [{'instant': 1, 'date': '2011-01-01 00:00:00,000000', 'season': 1, 'yr': 0, 'mnth': 1, 'weekday': 6, 'weathersit': 2, 'temp': 0.344167, 'atemp': 0.363625, 'hum': 0.805833, 'windspeed': 0.160446, 'casual': 331, 'registered': 654 }]}
Headers passed in (total 12):
    Host: localhost:5001
    X-Real-Ip: 127.0.0.1
    X-Forwarded-For: 127.0.0.1
    X-Forwarded-Proto: http
    Connection: close
    Content-Length: 812
    User-Agent: ApacheBench/2.3
    Accept: */*
    Authorization: Bearer q8szMDbCoNlxDZCpiGI8tnqaxtC1yDiy
    Content-Type: application/json
    X-Ms-Request-Id: 7cb6f8b9-e511-43b7-982f-e413d6e3239d
    Accept-Encoding: gzip
Scoring Timer is set to 60.0 seconds
200
```

---

## Key Benefits of Compute Instances

* Compute Instances are a managed, cloud-based workstation. It can be used in Azure Machine Learning Studio. This is a great way to take advantage of preloaded machine dependencies and not being responsible for their management.

#### New terms

* Compute Instance: A distinct type of a compute offering from Azure

* Cloud-based workstation: Sometimes, compute instances are referred to as a cloud-based workstation because it is ready to start developing

#### Further reading

* Azure's documentation on "What is a compute instance" defines some other key features of their offering.

* https://docs.microsoft.com/en-us/azure/machine-learning/concept-compute-instance


---

## Glossary

* ACI: Azure Container Instance

* AKS: Azure Kubernetes Service

* Application Insights: A special Azure service which provides key facts about an application

* CI/CD: Continuous Integration and Continuous Delivery platform. Jenkins, CircleCI, and Github Actions, are a few examples

* Cloud-based workstation: Sometimes, compute instances are referred to as a cloud-based workstation, because it is ready to start developing

* Compute Instance: A distinct type of a compute offering from Azure

* DevOps: A set of best practices that helps provide continuous delivery of software at the highest quality with a constant feedback loop

* Deployment: A way to deliver work into production

* Endpoint: A part of an HTTP API. Either a full URL or a partial URL identifying a part

* HTTP API: A URL that exposes logic to interact with software, in this case, a trained model

* HTTP Status code: A number that represents a status when an HTTP server responds. Error conditions in the server side start at 500

* Logging: Informational output produced by software, usually in the form of text

* Shipping into production: The most important aspect of a Machine Learning specialist

* Webservice: One of the most used Python classes from Azure's Python SDK


---

## Further Reading

These are some interesting links related to DevOps, CI/CD, and configuration in Azure ML Studio:

* Chapter 7 of Python For DevOps has an excellent section about logging and troubleshooting

* Both the Jenkins and Github Actions websites have good information about their CI/CD platforms and why they are compelling

* Azure's tutorial for how to setup authentication goes into some key details of the deployment configuration
(https://docs.microsoft.com/en-us/azure/machine-learning/how-to-setup-authentication)

* Azure's documentation has a whole section on monitoring and collecting data with Application Insights
(https://docs.microsoft.com/en-us/azure/machine-learning/how-to-enable-app-insights)

* The troubleshoot deployment of models section of Azure's documentation covers some of these troubleshooting concepts in detail
(https://docs.microsoft.com/en-us/azure/machine-learning/how-to-troubleshoot-deployment)

* Azure's documentation on "What is a compute instance" defines some other key features of their offering
(https://docs.microsoft.com/en-us/azure/machine-learning/concept-compute-instance)

---






























