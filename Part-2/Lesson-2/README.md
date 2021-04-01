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
A “Service Principal” is a user role with controlled permissions to access specific resources. Using a service principal is a great way to allow authentication while reducing the scope of permissions, which enhances security.

New terms
CI/CD: Continuous Integration and Continuous Delivery platform. Jenkins, CircleCI, and Github Actions are a few examples.


























































