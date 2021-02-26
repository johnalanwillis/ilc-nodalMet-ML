# Applying cloud computing resources to digital pathology 

## Table Of Contents
* [Introduction to Cloud Resources](#overview)
* [Setting up a google cloud account and using the cloud SDK](#digital-pathology-and-invasive-lobular-carcinoma)
* [Creating Virtual Machines and Accessing Storage](#project-organization-and-navigation)
* [Using Your Virtual Machine to perform image analysis](#project-organization-and-navigation)

## Introduction to Cloud Resources
As virtualization has matured and the volumes of data to be analyzed has exploded, many prominent technology companies began to repurpose the expertise they developed in datacenter and server design, offering the consumer access to small chunks of their excess computing resources. Over time, these cloud services have become major profit centers. Microsoft's Azure platform, the google cloud, and amazon's AWS products all offer highly scalable storage, computation, and coordination resources. The convenience of offloading the complexity of maintaining these resources allows businesses, consumers, and researchers the ability to focus on the design of the actual tasks to be performed, rather than configuring the often finicky resources necessary to support computation. 
While most research groups use local or university associated clusters for their computational work, the convenience and power of the cloud make it an increasingly appealing option for computationally focused research. 
The Google, Amazon, and Microsoft all offer generous free trials of their cloud services for consumers. Google offers 300 hours of compute time free, while microsoft offers 750 hours, and Amazon offers 750 hours per month for 1 year, with some limitations on storage capacity at the free tier. 
This work was performed on google cloud services, though the actual pipeline is essentially platform independent. There are minor differences in the terminology used to describe the services available on these platforms, but the structures are the same across platforms. Resources can be divided into 3 categories: Compute, storage, and coordination, each with major room for configuration based on the use case. In performing biological and ML tasks, a jobs-based approach with the ability to spin up and shut down compute resources as needed is most economical, and is simple to configure. 

## Setting up a google cloud account and using the cloud SDK
The Google Cloud Platform is accessible to anyone with a google account. The platform itself offers both a gui, a command line based SDK, and an API in many commonly used languages. While the GUI is the most approachable entree into google cloud services, the command line SDK offers better reproducibility and clarity for those comfortable with basic operation of command line interfaces. 
Use of the SDK is very simple. Once a google cloud account has been activated, the SDK can be downloaded and installed as described at https://cloud.google.com/sdk/docs/install. 
Once installed the SDK only needs to be linked with the user account to access compute resources. Access to storage resources requires the additional installation of gsutils, which provides a suite of addtional tools for the sdk, including access to storage buckets for unstructured data. 

Once the SDK and any additional tools have been installed, the SDK can be activatied with
`gcloud init`
which allows you to link the SDK to your google cloud account and perform additional configuration, including setting default locations for resources and setting up encrypted logins
further configuration options can be set with the command 
`gcloud config set <someOption>`
if a project already exists, perhaps if already created on the GUI, the project can be set within the SDK with 
`gcloud config set project <projectID>`

Further interaction with the project is carried out through the gcloud interface analogously to those commands listed above
commands follow a simple structure of 
`application(gcloud/gsutil) type operation --flags inputs/output`

## Creating Virtual Machines and Accessing Storage
Once a cloud account has been obtained, the SDK has been installed, and the SDK has been linked to an account an project, it can be used to create, manipulate, and shut down computational resources as needed. 
A simple and familiar application of compute resources is the creation of Virtual Machines. A Virtual machine functions identically to a personal computer, but rather than being tied to local physical resources, the machine can be configured at startup to suit the task at hand and destroyed when no longer needed. Virtual Machines can be configured in nearly any way that might be desired. Different processor architectures, storage volumes operating systems and program loadouts can be chosen at startup time and while some edits are possible to a running or paused machine, it is also simple to create a new, differently configured machine if the project parameters change and transfer the code and necessary data to the new VM. 

There are many ways to create a VM, from plug-and-play configurations to bare virtual machines that may be built up as they operate. Users may choose to load pre-configred "images" to their virtual machines, which ensures that all desired applications and configurations and compatible without need for configuration. These images may be hosted by google, obtained from a 3rd party image repository like dockerhub, or created from a manually configured VM with the "snapshot" function. Images allow users to maintain their working environment across the diverse architechtures offered, as the virtualization layer abstracts away hardware differences between compute configurations, with some limitations(Switching between CPU/GPU/TPU processing may require more tweaking). 

To create a virtual machine, we can use the GUI or the cloud SDK. It is worthwhile to use the GUI to search for premade images in the cloud marketplace, accessible from the sidebar in the cloud dashboard. From the marketplace, a search for "Deep Learning" images returns 41 results, capable of serving diverse use cases. Deploying one of these marketplace resources is as simple as selecting the image, clicking launch, and configuring the hardware and networking functions. The resulting VM can be accessed via ssh from a local cloud sdk or the cloud terminal built into the GUI. 
The SDK allows for simple and scriptable deployments of VMs when the desired configurations are known. 
available images can be searched with the command: 
`gcloud compute images list`
The desired image can then be configured and deployed with: 
`gcloud compute instances create VM_NAME \
    [--image IMAGE | --image-family IMAGE_FAMILY] \
    --image-project IMAGE_PROJECT`
and the successful deployment of the image can be confirmed with 
`gcloud compute images describe VM_NAME \
    --project IMAGE_PROJECT`
As with the GUI-created VMs, we can access the newly spun up resources with 
`gcloud compute ssh example-instance --zone=us-central1-a -- -vvv -L 80:%INSTANCE%:80`
This example accesses `example-instance` with port-forwarding configured on port 80

Once on the VM, it can be interacted with like any other computer. Programs can be installed, operations can be performed, data can be written and removed. 
One significant complication of working with VM's is the potential lack of persistent data. While VM's can have persistent storage associated with them, to be truly modular it is better to use offsite data storage and only copy over or stream the data as needed. To do this, further configuration is needed to allow a compute instance to communicate with a storage instance like a data storage bucket. 

Service accounts are used to link different cloud resouces. The VM user cannot simply walk into cloud storage or other resources as a matter of security. Best practices dictate that accounts, like those used to interact with a VM, have the minimal permissions needed to operate. To allow the VM to communicate with storage, a "service account" with the appropriate permissions must be linked to the VM. 
A new service account can be created from the IAM tab on the dashboard or from the SDK using the following command: 
`gcloud iam service-accounts create SERVICE_ACCOUNT_ID \
    --description="DESCRIPTION" \
    --display-name="DISPLAY_NAME"`

Once created, a service account can be further configured to give it explicit permissions using: 
`gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="serviceAccount:SERVICE_ACCOUNT_ID@PROJECT_ID.iam.gserviceaccount.com" \
    --role="ROLE_NAME"`

Proper configuration of a service account can be confirmed with: 
`gcloud iam service-accounts list`

Once configured, a service account can then be linked to a VM with: 
`gcloud compute instances set-service-account [INSTANCE_NAME] \
   [--service-account [SERVICE_ACCOUNT_EMAIL] | --no-service-account] \
   [--no-scopes | --scopes [SCOPES,...]]`

In this work, a service account was used to allow VMs to communicate with collections of histo image patches and WSI stored as objects in cloud storage buckets
most cloud providers offer resources for the storage and manipulation of structured and unstructured data. A bucket is used to store unstructured data objects, which can then be accessed as needed or copied over to a VM for manipulation. 
Interaction with cloud storage uses the gsutil suite
A cloud bucket can be created with: 
`gsutil mb [-b (on|off)] [-c <class>] [-l <location>] [-p <proj_id>]
          [--retention <time>] gs://<bucket_name>...` 

Onces created, a bucket can be interacted with similar to through lftp


## Using the cloud to perform Digital Pathology Image Analysis 
Configuring cloud resources takes some time in the beginning, but once comfortable, a user can rapidly deploy images linked to storage resources and perform computation as desired. 
In this work, a VM based on the Deep Learning image https://console.cloud.google.com/marketplace/product/click-to-deploy-images/deeplearning, the VM was linked to a service account with read/write access to a cloud storage bucket containing histopathology images. 
The VM was used to host a jupyter notebook, from which prototyping and small scale analysis was performed. 
For resource intensive jobs, or those with unclear needs, Cloud Dataproc offers a SLURM-like job submission interface. Pipelines developed interactively in notebooks hosted on cloud VMs were converted to job scripts submitted to a dataproc cluster. 
