# Cloud Pak For Business Automation Installation - Demo Version
## CP4BA Components
1) FileNet Content Manager 
2) Operational Decision Manager 
3) Automation Decision Services 
4) Business Automation Application 
5) Business Automation Workflow and Automation Workstream Services
6) IBM Automation Document Processing

## Table of Contents
1. Introduction
2. Pre-requisites(20.x)
3. Part One : Setup Admin Cluster
4. Part Two : Deploy Capabilites
5. Part Three : Generate URLs and Login Credentials

### Introduction
IBM Cloud Pak for Business Automation is a set of integrated market-leading software designed to help you solve your toughest operational challenges. With AI-generated recommendations, analytics to measure impact, and business-friendly low-code tooling, we've helped clients reduce the amount of time spent on manual processes by 90%¹ and decreased customer wait times by half². You can now better comply with regulations to reduce risk and save thousands of work hours that can then be reallocated to higher value work³.

### Pre-requisites(20.x)
1. Create ROKS Cluster </br>
   - You will need at least 3 worker nodes 8x32 </br>
   - [Review Cluster Requirements](https://www.ibm.com/docs/en/cloud-paks/cp-biz-automation/20.0.x?topic=deployment-identifying-infrastructure-requirements)
2. You will require registry key. It can be obtained using following link.</br>
   - [Generate Registry Key](https://myibm.ibm.com/products-services/containerlibrary)


## Part One : Setup Admin Cluster

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
       _(1) RedHat OpenShift Kubernetes Service (ROKS) - Public Cloud </br>
       (2) Openshift Container Platform (OCP) - Private Cloud </br>
       (3) Other ( Certified Kubernetes Cloud Platform / CNCF)_ </br>
6. What type of deployment is being performed? </br>
       _(1) Demo </br>
       (2) Enterprise_ </br>
7. Here are the existing users on this cluster: </br>
       _(1) IAM#gyalgin.sherpa@ibm.com_ </br>
       _Enter an existing username in your cluster, valid option [1 to 1], non-admin is suggested:_ `1`
8. Create storage classes for deployment: Done </br>
   `( Note: Storage class will be automatically created)`
9. Take note of the host name or you can get one using following commands
 ```console
        oc get route console -n openshift-console -o yaml|grep routerCanonicalHostname
 ```
10. Take note of the "Summary of input" </br>
         _(1) Cloud platform to deploy: ROKS 4.X </br>
         (2) Project to deploy: gs-cp4ba-baw </br>
         (3) User selected: IAM#gyalgin.sherpa@ibm.com </br>
         (5) Storage Class created: </br>
            cp4a-file-retain-bronze-gid </br>
            cp4a-file-retain-silver-gid </br>
            cp4a-file-retain-gold-gid_ </br>
   
## Part Two : Deploy Capabilities
1. Run deployment scripts
   ```console
      ./cp4a-deployment.sh
   ```
2. Do you accept the IBM Cloud Pak for Automation license (Yes/No, default: No): `Yes` </br>
3. Do you accept (Yes/No, default: No): `Yes` </br>
4. Password: `(Enter your pc login password)`</br>
5. Is this a new installation or an existing installation?</br>
      _(1) New </br>
      (2) Existing_ </br>
 6. Are you using the OCP Catalog (OLM) to perform this install? (Yes/No, default: No): `No`</br>
 7. What type of deployment is being performed?</br>
      _(1) Demo</br>
      (2) Enterprise_ </br>
 8. Select the cloud platform to deploy:</br>
      _(1) RedHat OpenShift Kubernetes Service (ROKS) - Public Cloud</br>
      (2) Openshift Container Platform (OCP) - Private Cloud_</br>
 9. Select the Cloud Pak for Automation capability to install:</br>
       _(1) FileNet Content Manager</br>
       (2) Operational Decision Manager</br>
       (3) Automation Decision Services</br>
       (4) Business Automation Application</br>
       (5) Business Automation Workflow and Automation Workstream Services</br>
       (6) IBM Automation Document Processing_ </br>
      
> Note: Press entry multiple times, if you have selected your capabilities.</br>

10. Do you have a Cloud Pak for Automation Entitlement Registry key (Yes/No, default: No): `Yes`</br>
11. Enter your Entitlement Registry key: `<copy the registry key here> refer to Pre-requisites point #2`</br>
12. Input the host name: `<copy the hostname here>refer to Part One point #9`</br>
13. Please enter the dynamic storage classname for slow storage: `<copy storage class here> refer to Part One point #10` </br>
14. Please enter the dynamic storage classname for medium storage: `<copy storage class here> refer to Part One point #10` </br>
15. Please enter the dynamic storage classname for fast storage: `<copy storage class here> refer to Part One point #10` </br>
16. To make changes, enter "No" (default: No): `Yes`</br>

## Part Three : Generate URLs & Login Credentials 
> Note: Pleas wait about 3-4 hours to complete the installation before executing the post deployment script.</br>
1. Run the post deployment script to get URLs and login crendials
   ```console
      ./cp4a-post-deployment.sh
   ```
2. Browse the require URLs with provided credentials to test the dashboard
