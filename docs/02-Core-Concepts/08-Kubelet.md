# Kubelet
  - Take me to [Video Tutorial](https://kodekloud.com/topic/kubelet/)
  
In this section we will take a look at kubelet.

#### Kubelet is the sole point of contact for the master node to the worker nodes in kubernetes cluster
- Kubelet loads or unloads the pods from the worker nodes as instructed by the scheduler on the master node.
- Kubelet also sends back the reports of the status of the worker nodes and pods on them at regular intervals to master node.
- Kubelet in the kubernetes worker nodes registers the nodes with the kubernetes cluster.
- When kubelet recieves instructions to load a pod on a node, it requests the container runtime engine to pull the required image and run an instance.
- Kubelet continues to monitor the nodes and pods and report to kube-apiserver on a timely basis. 
- The **`kubelet`** will create the pods on the nodes, the scheduler only decides which pods goes where.

  ![kubelet](../../images/kubelet.PNG)
  
## Install kubelet
- Kubeadm does not deploy kubelet by default. You must manually download and install it.
- Download the kubelet binary from the kubernetes release pages [kubelet](https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kubelet). For example: To download kubelet v1.13.0, Run the below command.
  ```
  $ wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kubelet
  ```
- Extract it
- Run it as a service

  ![kubelet1](../../images/kubelet1.PNG)
  
## View kubelet options
- You can also see the running process and affective options by listing the process on worker node and searching for kubelet.
  ``` 
  $ ps -aux |grep kubelet
  ```
  
  ![kubelet2](../../images/kubelet2.PNG)

K8s Reference Docs:
- https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/
- https://kubernetes.io/docs/concepts/overview/components/
- https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/kubelet-integration/
