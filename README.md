### Installing Kibana on IBM Cloud
This document will describe how to install Kibana on IBM Cloud using Kubernetes services.

### Contents

1. Introduction
2. Provision Kubernetes Cluster
3. Deploy IBM Cloud Block-Storage Plugin
4. Deploy Kibana
5. Verifying the Kibana Installation

### Introduction
To complete this tutorial, you should have an IBM Cloud account, if you do not have one, please [register/signup here](https://cloud.ibm.com/registration).
For installing Kibana, we have used the Kubernetes cluster, and used the IBM Cloud Block-Storage plugin for our persistent volume. Upon the completion of this tutorial, you would have the HashiCorp Consul up and running on the Kubernetes cluster.

1. Provision the Kubernetes cluster, if you have already setup one, skip to step 2.
2. Deploy the IBM Cloud Block-Storage Plugin to the created cluster, if you have already done this, skip to step 3.
3. Deploy the Kibana.

### Provision Kubernetes Cluster
* Click on the **Catalog** button on top center. Open [Catalog](https://cloud.ibm.com/catalog). ![alt text](Kubernetes1.png)

* In search catalog box, search for **Kubernetes Service** and click on it. ![alt text](Kubernetes2.png)

* You are now at Create Kubernetes Cluster page, there you have the two plans to create the Kubernetes cluster, either using **free plan** or **standard plan**.

**Option1- Using Free Plan:**
* Select Pricing Plan as “**Free**”. ![alt text](Kubernetes3.png)
* Click on **Create**.
* Wait a few minutes, and then your Cloud would be ready.

>**Note**: _Please be careful when choosing free cluster, as your pods could be stuck at pending state due to insufficient compute and memory resources, if you face such kind of issue please increase your resource by creating them choosing the standard plan._

**Option2- Using Standard Plan:**
* Select Pricing Plan as “**Standard**” 
* Select your **Kubernetes Version** as latest available or desired one by application. In our example we have set it to be '**1.18.14**'. 
  ![alt text](Kubernetes4.png)
  
* Select Infrastructure as “**Classic**”

  ![alt text](Kubernetes5.png)

* Leave Resource Group to “**Default**”
* Select Geography as “**Asia**” or your desired one.
* Select Availability as “**Single Zone**”.
>_This option allows you to create the resources in either single or multi availability zones. Multi availability zone provides you the option to create the resources in more than one availability zones so in case of catastrophe, it could sustain the disaster and continues to work._
* Select Worker Zone as **Chennai 01**.
* In Worker Pool, input your desired number of nodes as “**3**” ![alt text](Kubernetes6.png)
* Leave the Encrypt Local Disk option to “**On**”
* Select Master Service Endpoint to “**Both private and public endpoints**”
* Give your cluster-name as “**Kibana-Cluster**”
* Provide tags to your cluster and click on **Create**.
* Wait a few minutes, and then your Cloud would be ready.

  ![alt text](Kubernetes7.png)

### Deploy IBM Cloud Block-Storage Plugin
* Click on the **Catalog** button on top center.
* In search catalog box, search for **IBM Cloud Block Storage Plug-In** and click on it ![alt text](Storage1.png)
* Select your cluster as "**Kibana-Cluster**"
* Provide Target Namespace as “**kibana-storage**”, leave name and resource group to **default value**. ![alt text](Storage2.png)
* Click on Install

### Deploy Kibana
* Again go to the **Catalog** and search for **Kibana**. 
  
  ![alt text](Kibana1.png)
  
* Provide the details as below. ![alt text](Kibana2.png)

*	Target: **IBM Kubernetes Service**
*	Method: **Helm chart**
*	Kubernetes cluster: **Kibana-Cluster(jp-tok)**
*	Target namespace: **kibana**
*	Workspace: **kibana-01-13-2021**
*	Resource group: **Default**
*  Click on **Additional Parameters** with **Default Values**, you can set the deployment values or use the default ones, we have used the default in this example.

* Click on **Install**.

### Verifying the Kibana Installation
* Go to the **Resources List** in the Left Navigation Menu and click on **Kubernetes** and then **Clusters** 
* Click on your created **Kibana-Cluster**. 

  ![alt text](KibanaVerify1.png)
  
* A screen would come up for your created cluster, click on **Actions**, and then **Web Terminal** ![alt text](KibanaVerify2.png)
* A warning will appear asking you to install the Web Terminal, click on **Install**.
* When the terminal is installed, click on the action button again and click on web terminal and type the following command in below command window. It will show you the workspaces of your cluster, you can see **Kibana** active.

```sh
     $ kubectl get ns 
```
![alt text](KibanaVerify3.png)
     

```sh  
     $ kubectl get service –n Namespace 
```
![alt text](KibanaVerify5.png)


The installation is done. Enjoy!
