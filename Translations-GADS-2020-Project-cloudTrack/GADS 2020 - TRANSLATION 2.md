# Lab:Getting Started with GKE

## Objectives

In this lab, you learn how to perform the following tasks:

•	Provision a Kubernetes cluster using Kubernetes Engine.

•	Deploy and manage Docker containers using kubectl.

## Steps:

### In the GCP Console, confirm that both of these APIs are enabled:

•	Kubernetes Engine API

•	Container Registry API


### Start a Kubernetes Engine cluster

 1. Open the cloud shell, assign a zone to a environmental variable called MY_ZONE

        export MY_ZONE=us-central1-a

 2. Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes
 
        gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

 3. After the cluster is created, check installed version of Kubernetes using the kubectl version command:

        kubectl version

 4. View your running nodes in the GCP Console, Your Kubernetes cluster is now ready for use.
 

### Run and deploy a container

 1.	From Cloud Shell prompt, launch a single instance of the nginx container

        kubectl create deploy nginx --image=nginx:1.17.10
Note: If you see any deprecation warning about future version you can simply ignore it for now and can proceed further.


 2. View the pod running the nginx container

        kubectl get pods

 3. Expose the nginx container to the Internet
 
        kubectl expose deployment nginx --port 80 --type LoadBalancer
Kubernetes created a service and an external load balancer with a public IP address attached to it. The IP address remains the same for the life of the service. Any network traffic to that public IP address is routed to pods behind the service: in this case, the nginx pod

 4. View the new service

        kubectl get services

 5. use the displayed external IP address to test and contact the nginx container remotely.
It may take a few seconds before the External-IP field is populated for your service. This is normal. Just re-run the kubectl get services command every few seconds until the field is populated.

 6.	Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.
 
 7.	Scale up the number of pods running on your service:
 
        kubectl scale deployment nginx --replicas 3
Scaling up a deployment is useful when you want to increase available resources for an application that is becoming more popular.

 8. Confirm that Kubernetes has updated the number of pods:
 
        kubectl get pods

 9.	Confirm that your external IP address has not changed:
 
        kubectl get services

 10. Return to the web browser tab in which you viewed your cluster's external IP address. 

 11. Refresh the page to confirm that the nginx web server is still responding.


