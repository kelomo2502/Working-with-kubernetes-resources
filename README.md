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

## Deploying a Minicube sample applicaton using YAML

Lets create a Minikube deployment and service using `kubectl`
