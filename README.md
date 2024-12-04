# Working-with-kubernetes-resources

This hands-on project provides a clear and practical introduction to managing resources in a Kubernetes cluster. From understanding essential concepts to hands-on exercises like  creating, configuring, and optimizing resources such as deployments, services and understanding the syntax of YAML Files.

A Kubernetes YAML file is a text file written in YAML syntax that describes and defines Kubernetes resources. YAML is a human-readable data serialization format that is commonly used for configuration files. In the context of Kubernetes, these YAML files serve as a declarative way to specify the desired state of the resources such as pods, container, service and deployment you want to deploy and manage within a Kubernetes cluster.

## Basic strucuture of YAML file

YAML uses indentation to represent the hierarchy of data, and it uses whitespace (usually spaces, not tabs) for indentation.

```yaml
key1: value1
key2:
  subkey1: subvalue1
  subkey2: subvalue2
key3:
  - item1
  - item2

```

## Data types

**Scalars:** Scalars are single value

- strings

```yaml
name: John Doe

```

- numbers

```yaml
age: 25

```

- Booleans

```yaml
is_student: true

```

**Collections:**

- Lists(Arrays)

```yml
fruits:
  - apple
  - banana
  - orange

```

**Maps(key-value pairs):**

```yml
person:
  name: Alice
  age: 30

```

**Nested strucutures:**

```yml
employee:
  name: John Doe
  position: developer
  skills:
    - Python
    - JavaScript

```

**Comments:**

```yml
# This is a comment
key: value

```

**Multi strings:**

```yml
description: |
  This is a multiline
  string in YAML.

```

**Anchor and aliases:**

```yml

first: &name John
second: *name

```

## Deploying application in kubernetes

In Kubernetes, deploying applications is a fundamental skill that every beginner needs to grasp. Deployment involves the process of taking your application code and running it on a Kubernetes cluster, ensuring that it scales, manages resources efficiently, and stays resilient. This hands-on project will give an insight to deploying application using Minikube, a lightweight, single-node Kubernetes cluster perfect for beginners.

## Deployment in kubernetes

 Deployment in kubernetes is a declarative approach to managing and scaling applications. It provides a blueprint for the desired state of the application, allowing Kubernetes to handle the complexities of deploying and managing replicas. Whether it is running a simple web server or a more complex microservices architecture, Deployments are the cornerstone for maintaining application consistency and availability.

## Services in kubernetes

In Kubernetes, a Service is an abstraction that defines a logical set of Pods and a policy by which to access them. It acts as a stable endpoint to connect to the application, allowing for easy communication within the cluster or from external sources. Some of the several types of Services in Kubernetes;

- ClusterIp
  The default type. Exposes the Service on a cluster-internal IP. Accessible only within the cluster.

- NodePort
   Exposes the Service on each Node's IP at a static port (NodePort). Accessible externally using `NodeIP`

- Loadbalancer
   Exposes the Service externally using a cloud provider's load balancer. Accessible externally through the load balancer's IP.

## Deploying a Minikube sample applicaton using YAML

Lets create a Minikube deployment and service using `kubectl`

```bash
kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
```

The command above creates a Kubernetes Deployment named "hello-minikube" running the "kicbase/echo-server:1.0" container image

```bash
kubectl expose deployment hello-minikube --type=NodePort --port=8080

```

The command above exposes the Kubernetes Deployment named "hello-minikube" as a NodePort service on port 8080

```bash
kubectl get services hello-minikube

```

The easiest way to access this service is to let minikube launch a web browser for you
`minikube service hello-minikube`

## Working with YAML file

  1. Create a folder `my-nginx-yaml`
  2. Create a file `nginx-deployment-yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-nginx
  template:
    metadata:
      labels:
        app: my-nginx
    spec:
      containers:
      - name: my-nginx
        image: kelomo2502/gbnginx:1.0
        ports:
        - containerPort: 80


```

The provided YAML snippet defines a Kubernetes Deployment for deploying an instance of the Nginx web server. Let's break down the key components:

- **apiVersion: apps/v1**  Specifies the Kubernetes API version for the object being created, in this case, a Deployment in the "apps" group

- **Kind: Deployment**  Defines the type of Kubernetes resource being created, which is a Deployment. Deployments are used to manage the deployment and scaling of applications.
- **Metadata:**  Contains metadata for the Deployment, including the name of the Deployment, which is set to "my-nginx-deployment."
- **Spec:**  Describes the desired state of the Deployment.
- **Replica: 1**  Specifies that the desired number of replicas (instances) of the Pods controlled by this Deployment is 1.
- **Selector:**  Defines how the Deployment selects which Pods to manage. In this case, it uses the label "app: my-nginx" to match Pods.
- **Containers:**  Defines the containers within the Pod.
- **name: my-nginx:**  Sets the name of the container to "my-nginx."
- **image: kelomo2502/gbnginx:1.0**  Specifies the Docker image to be used for the Nginx container. The image is "kelomo2502/gbnginx" with version "1.0."
- **Ports:**  Specifies the port mapping for the container, and in this case, it exposes port 80.
  3.  Create a new file called `nginx-service-yaml` and paste the content below

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nginx-service
spec:
  selector:
    app: my-nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: NodePort


```

The provided YAML snippet defines a Kubernetes Service for exposing the Nginx application to the external world. Let's break down the key components:

- **apiVersion: v1**  Specifies the Kubernetes API version for the object being created, in this case, a Service.
- **kind:Service**  Defines the type of Kubernetes resource being created, which is a Service. Services provide a stable endpoint for accessing a set of Pods.
- **metadata:**  Contains metadata for the Service, including the name of the Service, which is set to "my-nginx-service."
- **spec:**   Describes the desired state of the Service.
- **selector:**  Specifies the labels used to select which Pods the Service will route traffic to. In this case, it selects Pods with the label "app: my-nginx."
- **ports**  Specifies the ports configuration for the Service.
- **protocol: TCP**  Specifies the ports configuration for the Service.
- **port: 80**  Specifies the ports configuration for the Service.
- **targetPort: 80**  Specifies the port on the Pods to which the traffic will be forwarded.
- **type: NodePort**  Sets the type of the Service to NodePort. This means that the Service will be accessible externally on each Node's IP address at a static port, which will be automatically assigned unless specified.

## Run the command below for the deployment on the cluster

`kubectl apply -f nginx-deployment.yaml`

`kubectl apply -f nginx-service.yaml`

## Verify your deployment

`kubectl get deployments`

`kubectl get services`

## Access your deployment

`minikube service my-nginx-service --url`
