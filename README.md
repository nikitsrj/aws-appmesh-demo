# aws-appmesh-demo
This repository includes sample app and appmesh config for the aws meetup demo

##Pre-requisites
1. EKS Cluster
2. Latest AWS CLI

## Steps for V1
1. Create the service mesh and its components for all the microservices

```
cd appmesh-config
./create-mesh.sh
```

2. Deploy Services in Kubernetes Cluster

```
cd ../k8s-deploy
./deploy_v1.sh
```

3. Deploy Curler to check the output of services

```
kubectl run -it curler --image=tutum/curl --env="SERVICES_DOMAIN=default.svc.cluster.local" bash

somercurleridbash# curl http://order.default.svc.cluster.local:5000

```
This should show the output of all the three services.

##Canary checking

### Deploy v1.5 of Customer SVC
1. Deploy services of v1.5 in EKS cluster
```
./deploy_v15.sh
```
2. Deploy appmesh config for canary
```
cd ../appmesh-config
./deploy-canary-v15.sh
```
Here you will see the change in output of CustomerSVC 

### Deploy v2 of Product SVC
1. Deploy services of v2 in EKS cluster
```
cd ../k8s-deploy
./deploy_v2.sh
```
2. Deploy appmesh config for canary
```
cd ../appmesh-config
./deploy-canary-v2.sh
```

## Cleanup the Service Mesh and Deploys

1. Cleaning up appmesh

```
cd appmesh-config
./delete-mesh.sh
```
2. Delete K8s Deploys
```
cd k8s-app
./remove_deploys.sh
```




