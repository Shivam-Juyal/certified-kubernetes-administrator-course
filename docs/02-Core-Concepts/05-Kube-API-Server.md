# Kube API Server
  - Take me to [Video Tutorial](https://kodekloud.com/topic/kube-api-server/)
  
In this section, we will talk about kube-apiserver in kubernetes

#### Kube-apiserver is the primary component in kubernetes.
- Kube-apiserver is primary management component in K8s.
- When we run a ```kubectl``` command, the kubectl utility is reaching kube-apiserver. The kube-apiserver first authenticates the request and validates it.
- It then retrives the data from the ETCD cluster and responds back with the requested information.


#### Creation of a pod
- We need not use ```kubectl``` to make pods.
- We can also call apis directly through ```post``` requests such as ```curl -X POST /api/v1/namespaces/default/pods ...[other]```.
- The request is first authenticated and then validated.
- The api server creates a pod object without assigning it to a node.
- api server updates the information in the ETCD server and also updates the user that the pod has been created.
- Scheduler continously monitors the kube-apiserver and realises that there is a new pod with no nodes assigned.
- The scheduler identifies the right node to place the new pod on, and communicates that back to the kube-apiserver.
- The kube-apiserver then updates the information on the etcd cluster and then passes the information to the kubelet of the appropriate worker node.
- Kubelet then creates the pod on the node and instructs the container runtime engine to deploy the application image.
- Once done, kubelet updates the status back to the kub-apiserver and the kube-apiserver then updates the data back to the ETCD cluster.

---
- A similar pattern is followed everytime a change is requested.
- Kube-apiserver is at the center of all the different tasks that needs to be performed to make a change in the cluster.
- **`IMPORTANT`**: Kube-apiserver is responsible for **`authenticating`**, **`validating`** requests, **`retrieving`** and **`Updating`** data in ETCD key-value store. In fact kube-apiserver is the only component that interacts directly to the etcd datastore. The other components such as kube-scheduler, kube-controller-manager and kubelet uses the API-Server to update in the cluster in their respective areas.
  
  ![post](../../images/post.PNG)
  
## Installing kube-apiserver

- If you are bootstrapping kube-apiserver using **`kubeadm`** tool, then you don't need to know this, but if you are setting up using the hardway then kube-apiserver is available as a binary in the kubernetes release page.
  - For example: You can downlaod the kube-apiserver v1.13.0 binary here [kube-apiserver](https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-apiserver)
    ```
    $ wget https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kube-apiserver
    ```
 
 ![kube-apiserver](../../images/kube-apiserver.PNG)
 
## View kube-apiserver - Kubeadm
- kubeadm deploys the kube-apiserver as a pod in kube-system namespace on the master node.
  ```
  $ kubectl get pods -n kube-system
  ```
   
  ![kube-apiserver1](../../images/kube-apiserver1.PNG)
   
## View kube-apiserver options - Kubeadm
- You can see the options with in the pod definition file located at **`/etc/kubernetes/manifests/kube-apiserver.yaml`**
  ```
  $ cat /etc/kubernetes/manifests/kube-apiserver.yaml
  ```
  
  ![kube-apiserver2](../../images/kube-apiserver2.PNG)
   
## View kube-apiserver options - Manual
- In a Non-kubeadm setup, you can inspect the options by viewing the kube-apiserver.service
  ```
  $ cat /etc/systemd/system/kube-apiserver.service
  ```
  
  ![kube-apiserver3](../../images/kube-apiserver3.PNG)
   
- You can also see the running process and affective options by listing the process on master node and searching for kube-apiserver.
  ```
  $ ps -aux | grep kube-apiserver
  ```
  ![kube-apiserver4](../../images/kube-apiserver4.PNG)

K8s Reference Docs:
- https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/
- https://kubernetes.io/docs/concepts/overview/components/
- https://kubernetes.io/docs/concepts/overview/kubernetes-api/
- https://kubernetes.io/docs/tasks/access-application-cluster/access-cluster/
- https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/
