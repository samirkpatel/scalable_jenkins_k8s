How to Setup Jenkins Distributed (Master-Slave) Build on Kubernetes.

Prerequisites:
- A working Kubernetes cluster, for this tutorial I’m using minikube.
- Kubernetes CLI (kubectl).
- I’m using jenkins (v2.237) image and jenkins slave (v4.3–1) image from official jenkins docker hub.

1. Setup Jenkins Deployment
   You can deploy Jenkins at any namespace, but for better isolation it is recommended that you create a dedicated namespace.

   cmd: kubectl create namespace jenkins

2. Create a Jenkins deployment that will assume role as master node, named jenkins-master.
   (Sample File Available inside jenkins-master folder).

3. Make sure these ports are open.
   - 8080  ---> Will be used for accessing jenkins API.
   - 50000 ---> will be used by Jenkins slave nodes (jnlp) and master node to communicate with each other.

Note: You can configure above setting with another port, but you need to reconfigure Jenkins for that purpose.

4.  Deploy the Jenkins by running below command.

    cmd: kubectl apply -f jenkins_deployment.yaml

5.  Add Kubernetes Service Account and Role for Jenkins.
    Jenkins needs to access the Kubernetes API, therefore you need to properly setup a Kubernetes Service Account and Role in order to represent Jenkins access for the Kubernetes API.

    - Create jenkins-master service account.
      basically you can achieve using 2 methods..
      1 - run below command to create a new service account.
          
          cmd: kubectl create serviceaccount jenkins-master -n jenkins
      
      2 - Write a service_account.yaml file with proper syntaxt and run kubectl apply. 
          (You can use service_account.yaml inside jenkins_master)

6.  Create required access Role and RoleBinding for jenkins-master service acount.







