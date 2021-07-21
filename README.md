# Cloud Pak For Business Automation Installation
## CP4BA Components
1) FileNet Content Manager (Selected)
2) Operational Decision Manager 
3) Automation Decision Services 
4) Business Automation Application (Selected)
5) Business Automation Workflow and Automation Workstream Services 
6) IBM Automation Document Processing (Selected)

## Table of Contents
1. Introduction
2. Pre-requisites(20.x)
3. Evaluation Deployment steps version 20.x
4. Evaluation deployment steps version 21.x
5. Verify Deployment

### Introduction
IBM Cloud Pak for Business Automation is a set of integrated market-leading software designed to help you solve your toughest operational challenges. With AI-generated recommendations, analytics to measure impact, and business-friendly low-code tooling, we've helped clients reduce the amount of time spent on manual processes by 90%¹ and decreased customer wait times by half². You can now better comply with regulations to reduce risk and save thousands of work hours that can then be reallocated to higher value work³.

### Pre-requisites(20.x)
1. Create ROKS Cluster </br>
   You will need at least 3 worker nodes 8x32 </br>
   <a href="https://www.ibm.com/docs/en/cloud-paks/cp-biz-automation/20.0.x?topic=deployment-identifying-infrastructure-requirements">Review Cluster Requirements </a>
2. You will require registry key. It can be obtained using following link.</br>
   <a href=https://myibm.ibm.com/products-services/containerlibrary> Generate Registry Key </a>


## Phase - 01 : Setup Admin Cluster

 1. Login to ROKS Cluster
 2. Clone Git Repository
      ```console
       git clone https://github.com/icp4a/cert-kubernetes.git
      ```
 3. Change directory to the scripts folder
      ```console
       cd cert-kubernetes/scripts
      ```
4. Run the cluster setup script and follow the instructions as it prompts 
      ```console
       ./cp4a-clusteradmin-setup.sh
      ```
5. Select the cloud platform to deploy: </br>
       (1) RedHat OpenShift Kubernetes Service (ROKS) - Public Cloud </br>
       (2) Openshift Container Platform (OCP) - Private Cloud </br>
       (3) Other ( Certified Kubernetes Cloud Platform / CNCF) </br>
6. What type of deployment is being performed? </br>
       (1) Demo </br>
       (2) Enterprise </br>
7. Here are the existing users on this cluster: </br>
       (1) IAM#gyalgin.sherpa@ibm.com ( Note: You will see your details displayed and select :1)</br>
8. Create storage classes for deployment: Done ( Note: Storage class will be automatically created)
9. Take note of the host name or you can get one using following commands
 ```console
        oc get route console -n openshift-console -o yaml|grep routerCanonicalHostname
 ```
10. Take note of the "Summary of input" </br>
         (1) Cloud platform to deploy: ROKS 4.X </br>
         (2) Project to deploy: gs-cp4ba-baw </br>
         (3) User selected: IAM#gyalgin.sherpa@ibm.com </br>
         (4) Storage Class created: </br>
            cp4a-file-retain-bronze-gid </br>
            cp4a-file-retain-silver-gid </br>
            cp4a-file-retain-gold-gid </br>
   
## Phase - 02 : Deploy Capabilities
1. Run deployment scripts
   ```console
      ./cp4a-deployment.sh
   ```
2. Do you accept the IBM Cloud Pak for Automation license (Yes/No, default: No): Yes </br>
3. Do you accept (Yes/No, default: No): Yes </br>
4. Password: (Enter your pc login password)</br>
5. Is this a new installation or an existing installation?</br>
      (1) New </br>
      (2) Existing </br>
 6. Are you using the OCP Catalog (OLM) to perform this install? (Yes/No, default: No): No</br>
 7. What type of deployment is being performed?</br>
      (1) Demo</br>
      (2) Enterprise </br>
 8. Select the cloud platform to deploy:</br>
      (1) RedHat OpenShift Kubernetes Service (ROKS) - Public Cloud</br>
      (2) Openshift Container Platform (OCP) - Private Cloud </i></br>
 9. Select the Cloud Pak for Automation capability to install:</br>
       (1) FileNet Content Manager</br>
       (2) Operational Decision Manager</br>
       (3) Automation Decision Services</br>
       (4) Business Automation Application</br>
       (5) Business Automation Workflow and Automation Workstream Services</br>
       (6) IBM Automation Document Processing</i></br>
      
Note: Press entry multiple times, if you have selected your capabilities.</br>

10. Do you have a Cloud Pak for Automation Entitlement Registry key (Yes/No, default: No): Yes</br>
11. Enter your Entitlement Registry key: <copy the registry key here></br>
12. Input the host name: <copy the hostname here></br>
13. Please enter the dynamic storage classname for slow storage: <copy storage class here> eg. cp4a-file-retain-bronze-gid</br>
14. Please enter the dynamic storage classname for slow storage: <copy storage class here> eg. cp4a-file-retain-bronze-gid</br>
15. Please enter the dynamic storage classname for slow storage: <copy storage class here> eg. cp4a-file-retain-bronze-gid</br>
16. To make changes, enter "No" (default: No): Yes</br>

## Phase - 03 : Post Deployment 
1. Run the post deployment script to get URLs and login crendials
   ```console
      ./cp4a-post-deployment.sh
   ```
2. Browse the require URLs with provided credentials to test the dashboard
