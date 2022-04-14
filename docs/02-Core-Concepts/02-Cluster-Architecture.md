# Cluster Architecture

  - Take me to [Video Tutorial](https://kodekloud.com/topic/cluster-architecture/)

In this section , we will take a look at the kubernetes Architecture at high level.
- 10,000 Feet Look at the Kubernetes Architecture
- The master node does all of the monitoring task using a set of components, together known as control plane components.
  - All the information about the nodes and the containers that they host, is stored in a highly available key-value store known as ETCD.
  - ETCD is a database that stores information in a key-value pair.
  - 

  ![Kubernetes Architecture](../../images/k8s-arch.PNG)
  
  ![Kubernetes Architecture 1](../../images/k8s-arch1.PNG)

K8s Reference Docs:
- https://kubernetes.io/docs/concepts/architecture/
