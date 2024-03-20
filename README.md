# WordPress-MySQL-K8s-Deployment
Just a simple K8s tutorial to get me started with container orchestration.

Kubernetes, often abbreviated as K8s (K-eight-s), is an open-source container orchestration platform originally developed by Google and now maintained by the Cloud Native Computing Foundation (CNCF). It automates the deployment, scaling, and management of containerized applications.

I decided to run Kubernetes because it's easier to deploy microservices and a great way of  managing your containers. 

***DISCLAIMER!***: this was deployed through minikube so change certain parts of
the yaml code to fit your needs.

***Step 1.0 Download the Repo:***

For this step you need git installed so go ahead and download it. when its done run:

```bash 
git clone https://github.com/eto330/WordPress-MySQL-K8s-Deployment.git
```
#### 1.0 Deployment: MySQL

***Step 1.1 Run the Secret yaml file for MySQL:***

This file it's an important way of using passwords without declaring sensitive data and its also a way of keeping them secure.

To run the secrets yaml file modify the `MYSQL_ROOT_PASSWORD` with the base64 password you want for the service.
An easy way of finding this is to run:
```bash
bash -n <your-password> | base64
```
Once you got that, copy the output and open the `mysql-secret.yml` file with your favorite editor (I recommend nano for beginners) and change the `MYSQL_ROOT_PASSWORD`  value to the base64 output.

run the command:
```bash
nano mysql-secret.yml
```
to open the file with nano. After doing the changes, go ahead and save the file by pressing Ctrl-x then y. Once you're done, apply it by running:
```bash
kubectl apply -f mysql-secret.yml
```
now the secret it's being enforce for later use.

to check the status of the secret we just deployed run:
```bash
kubectl get secret
```
***Step 1.2 Run the MySQL Persistent Volume File:***

Persistent volumes (PVs) in Kubernetes (K8s) serve a crucial role in managing storage for applications running in containers. Here are several reasons why persistent volumes are essential in Kubernetes: Data Persistence, Decoupling Storage from Pods, Data Sharing, etc.

First, modify the value array on the `mysql-pv.yml`  file from `minikube` to whatever node you're currently using.
When you are done, apply the changes:
```bash
kubectl apply -f mysql-pv.yml
```
then run:
```bash
kubectl get pv
```
to get the status of the volume.

***Step 1.3 Create MySQL Deployments***
We're now moving on to the deployments of the mysql service. this step it's a simpler one where you just have to apply the `mysql.yml` file just like the above bash command and you'll be set.

to check for the status run:

```bash
kubectl get pod
```
***Step 1.4 Create MySQL Service***


Services are an integral part of Kubernetes. Its how the traffic flow thru the network and what ports are open and so on. 
on this step we will be applying the `mysql-service.yml` with the following command.
```bash
kubectl apply -f mysql-service.yml
```

this command will check the availavility of the service:
```bash
kubectl get service
```
now we must go inside the kubernetes container and by running this command:
```bash
kubectl exec -it pod_name -- bash
```
once you are in you should run this command while also providing the sql root password given on step 1.1 (without base64) to log in into the database service. 
```bash
mysql -u root -p <password>
```
once you are logged in, you will need to create it. So go ahead and run the following command:
```bash
CREATE DATABASE wordpress;
```
to exit, just run:
```bash
exit
```

#### 2.0 Deployment: WordPress

***Step 2.1***








TODO: FINISH!!
