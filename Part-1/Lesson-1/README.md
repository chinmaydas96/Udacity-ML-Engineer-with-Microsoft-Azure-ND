![](screen1.png)

___


# Course Overview

## Lesson 1: Introduction to Azure Machine Learning

* **What You'll Build :**  We'll have a look at a preview of what you'll build on your final project.

* **Why Do ML in the Cloud :** We'll go over some key reasons why you would want to do Machine Learning (ML) in the cloud. We'll look into some of the limitations of performing ML locally on your machine, as well as how the cloud addresses these limitations.

* **When to Do ML in the Cloud :** Most of the time the cloud is your best option for ML. But we'll discuss a few edge cases in which using the cloud may not be the best route.

* **Customers of ML :** We'll look at the different customers of machine learning, including both internal and external customers.

---

## Lesson 2: Workspaces and AzureML Studio

* **The Azure ML Platform :** We'll talk about the core features of the Microsoft Azure ML platform and how they enable you to be more productive as a data scientist or machine learning engineer.

* **Workspaces and Notebooks :** Workspaces and notebooks are critical components of Microsoft Azure. We'll learn how these tools enable you to be a more effective data scientist—including the use of Jupyter to build and deploy machine learning models.

---

## Lesson 3: Datastores and Datasets
* **Datastores and Datasets :** Datastores and Datasets are a critical component of cloud computing. We'll learn how Azure allows you to easily integrate third party datasets and open datasets into our ML pipeline to quickly develop working solutions.

---

## Lesson 4: Training models in Azure
* **Managing pipelines :** We'll cover how to create a pipeline that you manage yourself using the console, which will alow you to make very small changes that can be run repeatedly.

* **Hyperparameters in experiments :** We'll learn how to use hyperparameters in experiments, including how we can automate the creation of hyperparameters and make very small changes that create huge value in terms of prediction accuracy.

---

## Lesson 5: Azure ML SDK

* **Creating pipelines :** We'll talk about how the Azure ML SDK allows us to programmatically create pipelines. By automating the creation of pipelines, we can create more pipelines; also, our pipeline creation becomes a a repeatable process that other members of our team can follow.

* **Managing experiments :** We'll learn how to use the SDK to manage experiments programmatically with Python, allowing us to easily rerun our processes using Python scripts.

---

## Lesson 6: Automated Machine Learning and Hyperparameter Tuning

* **Automated ML and SDK :**  We'll discuss how we can use the Azure ML SDK to do Automated ML and create models more quickly and accurately.

* **Model Interpretation:** We'll explore how model interpretation allows us to build solutions using Automated ML that we (and others) can more easily interpret, making visible the core features that are driving the model.

## Project: Creating and Optimizing an ML Pipeline

* In the project at the end of this course, you'll have the opportunity to create and optimize an ML pipeline. You'll do this both using HyperDrive and also Automated ML, so that you can compare the results of the two methods.

---
---
---

### Why Do Machine Learning in the Cloud

Although you can certainly do machine learning locally on your own machine, but this will involve limitations imposed by your machine's resources. In contrast, the cloud provides a variety of platform tools that are constantly being developed and improved by some of the best engineers in the world. In the Azure cloud, these include:

* **Data lakes**, which provide essentially infinite storage that is also very secure.

* **Machine Learning Studio**, which makes it easy to build a full, end-to-end ML solution, leveraging great ready-made resources like open datasets.

* **DevOps build systems**, allowing you to integrate DevOps pipelines with your machine learning workflows.

* **Serverless technology**, in which Azure runs the server and handles the provisioning of machine resources for you automatically, allowing you to more easily solve complex orchestration problems.


---

### When to Do ML in the Cloud


Most of the time the cloud is your best option for ML. Some reasons to favor cloud computing include:

* **Data governance :** Cloud solutions offer additional security to help prevent problems like data breaches and piracy.
Better ability to leverage new services. A cloud-native approach allows you to leverage new services as they're developed. You're betting on the future, knowing that the cloud platform will get a constant set of new features (in contrast to you needing to build those features yourself).
Even so, there are a few edge cases in which using the cloud may not be the best route. These include:

* **Legal/government requirements :** If your company handles sensitive data, such as medical records or government files, it may not be legally possible to move to the cloud.

* **Legacy applications :** If you have a legacy application that is currently working, but that is unlikely to be updated, it may not make sense to take the risk of moving it to the cloud.

* **Specialized HPC :** In some cases, you may already have a specialized and very expensive High Performance Computing (HPC) cluster. In such a case, it may be more cost effective to keep what you have and only use the cloud for some parts of your workflow.

---












