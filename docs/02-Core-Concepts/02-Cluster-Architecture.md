# Cluster Architecture

  - Take me to [Video Tutorial](https://kodekloud.com/topic/cluster-architecture/)

In this section , we will take a look at the kubernetes Architecture at high level.
- 10,000 Feet Look at the Kubernetes Architecture
- The master node does all of the monitoring task using a set of components, together known as control plane components.
  - All the information about the nodes and the containers that they host, is stored in a highly available key-value store known as ETCD.
  - ETCD is a database that stores information in a key-value format.
  
- ## Kube-scheduler
  - A scheduler identifies the right node to place a container on, based on the container's resource requirements, worker node capacity or any other policies or constraints.

- ## Controller-Manager
  - Node-Controller
  - Replication-Controller

- ## Kube-apiserver
  - Responsible for orchestrating all the operations within the cluster.
  - Exposes k8s api, which is used by external users to perform management operations on the cluster.
  
- ## Container Runtime Engine
  - Everything in k8s is containerized.
  - We need container runtime engine to run containers.
  - Docker: popular container runtime engine.
  - If we require every service to be containerized including the control plane components, we need to install the container runtime on every node including the master.
  
- ## Kubelet
  - Engine that runs on each node in the cluster.
  - It listens for the instructions from the kubeapi server and deploys or destroys the containers on the nodes as required.
  - Kube-apiserver periodically fetches the status reports from kubelet to monitor the status of nodes and the containers on them.

- ## Kube-proxy Service
  - It ensures that the necessary rules are in place on the worker nodes to allow the containers on them to reach each other.



  ![Kubernetes Architecture](../../images/k8s-arch.PNG)
  
  ![Kubernetes Architecture 1](../../images/k8s-arch1.PNG)

K8s Reference Docs:
- https://kubernetes.io/docs/concepts/architecture/
