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


