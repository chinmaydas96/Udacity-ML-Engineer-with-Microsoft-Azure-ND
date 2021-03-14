![](screen1.png)

---
# Lesson Overview

* **The Azure ML Platform :** We'll talk about the core features of the Microsoft Azure ML platform and how they enable us to be more productive as data scientists or machine learning engineers—including how elastic resources give us the power to do ML at scale.

* **Managing and choosing compute resources :** We'll explore the role of compute instances, compute clusters, inference clusters, and attached compute. We'll also consider the tradeoffs involved in choosing resources, such as GPU vs CPU, VM size, cluster size, and dedicated vs low-priority instances.

* **Workspaces and Notebooks :** Workspaces and notebooks are critical components of Microsoft Azure. We'll learn how these tools enable you to be a more effective data scientist—including the use of Jupyter to build and deploy machine learning models.


___

# Intro to Azure ML Platform

![1](screen2.png)

---

![2](screen3.png)

---

![3](screen4.png)

---

![4](screen5.png)


---

* The Azure ML platform is composed of two main components: 
	* The Azure Cloud  
	
	* Azure ML Studio.

* Key features of Azure Cloud include:

	* Scalable, on-demand compute instances.
	
	* Data storage and connectivity.

* Key features of Azure ML studio include:

	* The ability to easily orchestrate machine learning workflows.
	
	* Model registration and management (or MLOps). This allows you to register models or track them and control the lineage.
	
	* Metrics and monitoring, giving you the ability to look at the compute, the storage, or a training job, and make sure that it's running effectively.
	
	* Model deployment; you can create an inference end point and deploy your model so that it runs 24/7 and is elastically scaled to meet demand.




# Managing Compute Resources

Managing compute resources effectively involves several main components:

#### Compute instances

* A central component of managing compute resources involves the ability to spin up a Virtual Machine (VM), provision the correct resources for that VM, and then launch a notebook—which you can then use to control other components of your project, such as by calling out to a compute cluster.

#### Compute clusters

* A compute cluster is a specialized cluster of Virtual Machines used to train ML models at scale, adjusting elastically to the requirements. Compute clusters can also employ specialized GPU or CPU resources.

#### Inference clusters
* Inference clusters, as the name suggests, are used to establish a production ML endpoint and serve out predictions. Like compute clusters, inference clusters are also groups of Virtual Machines—and like compute clusters, they too can scale up and down in response to demand, thus ensuring that your customers always have a good response time. Inference clusters can be configured to do monitoring and logging, and set up to ensure that the model is running 24/7.

#### Attached compute

* Attached compute, or "unmanaged compute," allows you to do integration with third party services. Those third party services could be anything from your own VM to something like a data bricks cluster that does managed Spark. If you have experience with a tool from, say, a previous job, you can integrate that tool with Azure ML Studio and thus use that pre-existing skill in your pipeline.



![1](screen6.png)

---

![2](screen7.png)

---

![3](screen8.png)


---

# Choosing the Compute Resource for Your Needs

* When choosing the compute resources for your needs, some key factors to consider are GPU vs CPU, cluster size, VM size, and dedicated vs low-priority instances. Let's have a look at the factors involved in each of these choices.


### CPU vs GPU

* Characteristics of CPUs:

	* Less expensive
	* Lower level of concurrency (a CPU isn't designed for parallel computing)
	* Can be a lot slower in training deep learning models
	* If time really isn't a critical factor, it could be a good option to save

* Characteristics of GPUs

	* More expensive
	* Higher level of concurrency (GPUs are designed for parallel computing)
	* Optimal for deep learning
	* Used in both inference and training; the power level for these may be different


### Cluster Size

* The primary consideration with cluster size is response time:

	* If you have a cluster that starts at zero nodes, that means it will have to spin up a node when it is needed for a task, which could lead to slower response times (but will save on costs).

	* A larger starting cluster size will result in better responsiveness, but will also be more expensive.
	In sum, if you have more time, but less money, you may want to go with a smaller cluster size. Conversely, if you have less time and more money, you may want to go with a larger cluster size.


### VM Size

* The "size" of a VM can vary in terms of a number of features, including:

	* RAM
	* Disk size
	* Number of cores
	* Clock speed

* Getting a VM with more RAM, larger disk size, a greater number of cores, and higher clock speed, will result in better performance, but will also be more expensive. The choice depends on the training and inference needs of the problem you're trying to solve, as well as your time and budgetary constraints.

### Dedicated Instances vs Low-Priority Instances

* When an instance is low-priority this means it is interruptible—essentially, Microsoft Azure can take those resources and assign them to another task, thus interrupting a job.

* When an instance is dedicated, or non-interruptible, this means that the job will never be terminated without your permission.

* This is another consideration of time vs money, since interruptible instances are less expensive than dedicated ones.



















