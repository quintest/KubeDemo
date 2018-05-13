# KubeDemo
For more background info please goto the following site where the complete tutorial is written out, this a TLDR;-walkthrough.
[https://cloud.google.com/kubernetes-engine/docs/tutorials/persistent-disk#step_3_set_up_mysql](https://cloud.google.com/kubernetes-engine/docs/tutorials/persistent-disk#step_3_set_up_mysql)

Here you can also find the Manifest Yaml-files needed to follow along.

In the GCP Console carry out the following commands:

**Setup**

`gcloud config set compute/zone europe-west4-b`

`gcloud container clusters create persistent-disk-tutorial --num-nodes=3`

`gcloud compute disks create --size 200GB mysql-disk`

`gcloud compute disks create --size 200GB wordpress-disk`

`kubectl create secret generic mysql --from-literal=password=[YOUR_PASSWORD]`

**Demo Part 1**

make sure your in the right directory..

`kubectl create -f mysql.yaml`

`kubectl get pod -l app=mysql`

`kubectl create -f mysql-service.yaml`

`kubectl get service mysql`

`kubectl create -f wordpress.yaml`

`kubectl get pod -l app=wordpress`

`kubectl create -f wordpress-service.yaml`

`kubectl get svc -l app=wordpress -w`

**Browser Wordpress setup, connect to External IP**

--

**Demo Resilience**

`kubectl get pods -o=wide`

`kubectl delete pod -l app=mysql`

`kubectl get pods -o=wide`


**Cleanup**

`kubectl delete service wordpress`

`gcloud compute forwarding-rules list`

`gcloud container clusters delete persistent-disk-tutorial`

`gcloud compute disks delete mysql-disk wordpress-disk`
