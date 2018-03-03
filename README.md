# my-microservice-consumer
springoboot microservice consumer

# Build and create Docker Image

Assumptions:
1. mvn, docker are installed

```
git clone repo
mvn package
mvn install dockerfile:build
docker push klinakuf/my-microsercvice-consumer
```

Destroy pods to see updates in the Kubernetes cluster. 

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

# Install rabbitmq via helm

```
** Please be patient while the chart is being deployed **

  Credentials:

    echo Username      : user
    echo Password      : $(kubectl get secret --namespace default romping-opossum-rabbitmq -o jsonpath="{.data.rabbitmq-password}" | base64 --decode)
    echo ErLang Cookie : $(kubectl get secret --namespace default romping-opossum-rabbitmq -o jsonpath="{.data.rabbitmq-erlang-cookie}" | base64 --decode)

  RabbitMQ can be accessed within the cluster on port 5672 at romping-opossum-rabbitmq.default.svc.cluster.local

  To access for outside the cluster execute the following commands:

    export POD_NAME=$(kubectl get pods --namespace default -l "app=romping-opossum-rabbitmq" -o jsonpath="{.items[0].metadata.name}")
    kubectl port-forward $POD_NAME 5672:5672 15672:15672

  To Access the RabbitMQ AMQP port:

    echo amqp://127.0.0.1:5672/

  To Access the RabbitMQ Management interface:

    echo URL : http://127.0.0.1:15672
```
