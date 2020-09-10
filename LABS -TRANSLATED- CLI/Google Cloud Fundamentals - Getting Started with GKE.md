# Lab: Google Cloud Fundamentals: Getting Started with GKE

## Objectives:
In this lab, you will learn how to perform the following tasks:
 -  Provision a Kubernetes cluster using Kubernetes Engine.
 -Deploy and manage Docker containers using kubectl.

### Steps
1. Use assigned project ID, username and password to sign into qwiklabs using the incognito windows. 
2. Confirm that needed APIs are enabled.
  For your current default project, list all available APIs enabled by executing this command
    ```
gcloud service-management list --enabled 
```
Check the result to confirm that both of these APIs are enabled:
 - Kubernetes Engine API
 -Container Registry API
 
 If any of them is missing, enable them by this command prompt for each API:

  - To enable to Kubernetes Engine API
```     
gcloud services enable container.googleapis.com
```
  - To enable Container Registry API
   ```
 gcloud services enable containerregistry.googleapis.com
```   
3. Start a Kubernetes Engine cluster
  - Place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE. At the Cloud Shell prompt, type this partial command:
 ```
export MY_ZONE=
 ```
  - Include the zone qwiklabs indicated:
```
    export MY_ZONE=us-central1-a	
```  
  - Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster `webfrontend` and configure it to run 2 nodes:
```    
gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
```
  - After the cluster is created, check your installed version of Kubernetes using the kubectl version command:
```    
kubectl version
```  
Result: The gcloud container clusters create command automatically authenticated kubectl for you.
  
4. Run and deploy a container
    - From your Cloud Shell prompt, launch a single instance of the nginx container. 
```
kubectl create deployment nginx --image=nginx:1.17.10
``` 
    - View the pod running the nginx container:
```
kubectl get pods
```
    - Expose the nginx container to the Internet:
```
kubectl expose deployment nginx --port 80 --type LoadBalancer
```
  Result: Kubernetes created a service and an external load balancer with a public IP address attached to it. The IP address remains the same for the life of the service

  -   View the new service:  
```
kubectl get services
```
  Just re-run the kubectl get services command every few seconds until the field is populated. Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.
 - Scale up the number of pods running on your service:
```
    kubectl scale deployment nginx --replicas 3
```
 - Confirm that Kubernetes has updated the number of pods:
```   
 kubectl get pods
```
 - Confirm that your external IP address has not changed:
    ```
kubectl get services
```
 - Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.