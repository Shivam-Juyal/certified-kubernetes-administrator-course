# Kube Scheduler
  - Take me to [Video Tutorial](https://kodekloud.com/topic/kube-scheduler/)

In this section, we will take a look at kube-scheduler.

#### kube-scheduler is responsible for scheduling pods on nodes.  
- The kube-scheduler is only responsible for deciding which pod goes on which node. It doesn't actually place the pod on the nodes, that's the job of the **`kubelet`**.
- Scheduler makes sure that the correct pod goes into the correct node.
- In kubernetes, scheduler decides which nodes the pods are placed on, depending on certain criteria.
- The scheduler looks for each pod and tries to find the best node for it.
- Suppose the pod has a requirement of 10 cpu.
  - First phase : **Filter Nodes**
    - In this phase the scheduler filters out the nodes that could not accomodate the pod's requirement of 10 cpu.
  - Second phase : **Rank Nodes**
    - In this phase the scheduler ranks the nodes to identify the best fit for the pod. It uses a priority function to assign a score to nodes on a scale of 0 to 10. for example, the scheduler calculates the amount the resources that will be free on the nodes after placing the pod on them. The node with more free resources after placing the pod gets the better rank.      

  ![kube-scheduler1](../../images/kube-scheduler1.PNG)
  
#### Why do you need a Scheduler?

  ![kube-scheduler2](../../images/kube-scheduler2.PNG)
    
## Install kube-scheduler - Manual
- Download the kubescheduler binary from the kubernetes release pages [kube-scheduler](https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-scheduler). For example: To download kube-scheduler v1.13.0, Run the below command.
  ```
  $ wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-scheduler
  ```
- Extract it
- Run it as a service

  ![kube-scheduler3](../../images/kube-scheduler3.PNG)
  
## View kube-scheduler options - kubeadm
- If you set it up with kubeadm tool, kubeadm tool will deploy the kube-scheduler as pod in kube-system namespace on master node.
  ```
  $ kubectl get pods -n kube-system
  ```
- You can see the options for kube-scheduler in pod definition file that is located at **`/etc/kubernetes/manifests/kube-scheduler.yaml`**
  ```
  $ cat /etc/kubernetes/manifests/kube-scheduler.yaml
  ```
  ![kube-scheduler4](../../images/kube-scheduler4.PNG)
  
- You can also see the running process and affective options by listing the process on master node and searching for kube-apiserver.
  ``` 
  $ ps -aux | grep kube-scheduler
  ```
  ![kube-scheduler5](../../images/kube-scheduler5.PNG)
  
  K8s Reference Docs:
  - https://kubernetes.io/docs/reference/command-line-tools-reference/kube-scheduler/
  - https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/
  - https://kubernetes.io/docs/concepts/overview/components/
  - https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/
    
