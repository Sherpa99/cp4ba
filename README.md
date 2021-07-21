# Cloud Pak For Business Automation Installation
## CP4BA Components
### 1) FileNet Content Manager (Selected)
###	2) Operational Decision Manager 
###	3) Automation Decision Services 
###	4) Business Automation Application (Selected)
###	5) Business Automation Workflow and Automation Workstream Services 
###	6) IBM Automation Document Processing (Selected)

## Table of Contents
### Introduction
### Pre-requisites(20.x)
### Evaluation Deployment steps version 20.x
### Evaluation deployment steps version 21.x
### Verify Deployment


### Introduction
IBM Cloud Pak for Business Automation is a set of integrated market-leading software designed to help you solve your toughest operational challenges. With AI-generated recommendations, analytics to measure impact, and business-friendly low-code tooling, we've helped clients reduce the amount of time spent on manual processes by 90%¹ and decreased customer wait times by half². You can now better comply with regulations to reduce risk and save thousands of work hours that can then be reallocated to higher value work³.

### Pre-requisites(20.x)
1) Create ROKS Cluster
   You will need at least 3 worker nodes 8x32
   <a href=https://www.ibm.com/docs/en/cloud-paks/cp-biz-automation/20.0.x?topic=deployment-identifying-infrastructure-requirements)>Review Cluster Requirements </a>
2) You will require registry key. It can be obtained using following link.
   <a href=https://myibm.ibm.com/products-services/containerlibrary> Generate Registry Key </a>

### Evaluation Deployment steps version 20.x
    1) Login to ROKS Cluster
    2) Clone Git Repository
       ```console
       git clone https://github.com/icp4a/cert-kubernetes.git
       ```
    3) Change directory to the scripts folder
    ```console
       cd cert-kubernetes/scripts
    ```
    4) Run the cluster setup script and follow the instructions as it prompts
    ```console
       ./cp4a-clusteradmin-setup.sh
    ```
    5) Select the cloud platform to deploy:
       1) RedHat OpenShift Kubernetes Service (ROKS) - Public Cloud
       2) Openshift Container Platform (OCP) - Private Cloud
       3) Other ( Certified Kubernetes Cloud Platform / CNCF)
    6) What type of deployment is being performed?
       1) Demo
       2) Enterprise
    7) Here are the existing users on this cluster:
       1) IAM#gyalgin.sherpa@ibm.com ( Note: You will see your details displayed and select :1)
    8) Create storage classes for deployment: Done ( Note: Storage class will be automatically created)
    9) Take note of the host name or you can get one using following commands
       ```console
        oc get route console -n openshift-console -o yaml|grep routerCanonicalHostname
       ```
    10) Take note of the "Summary of input"
         1. Cloud platform to deploy: ROKS 4.X
         2. Project to deploy: gs-cp4ba-baw
         3. User selected: IAM#gyalgin.sherpa@ibm.com
         5. Storage Class created:
            cp4a-file-retain-bronze-gid
            cp4a-file-retain-silver-gid
            cp4a-file-retain-gold-gid
       
