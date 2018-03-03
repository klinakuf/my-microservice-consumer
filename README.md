# my-microservice-consumer
springoboot microservice consumer


# Deploy the service to Kubernetes

Assumptions:
1. A running Kubernetes Cluster
2. A working kubectl

Notes: 
- The image that is deployed in the cluster is obtained from docker repository, for the recent source a ```mvn docker:push``` is neccessary first

Steps:

```
kubectl apply -f artefacts/deployment.yaml artefacts/deployment.yaml
kubectl proxy
```
Access the service via the following url:

http://localhost:8001/api/v1/namespaces/default/services/my-ms-consumer/proxy/

