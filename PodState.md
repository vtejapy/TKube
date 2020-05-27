

# pod State
-----
- the different statuses and states of a pod and conteinr:
  - **pod status** field: high level  status
  - **pod condition**: the condition of the pod 
  - **container state**: state of the container(s) itself
 - pod have a status field, which you see when you do kubectl get pods:
 ```
[vagrant@kmaster ~]$ kubectl get pods -n kube-system
NAME                                          READY   STATUS    RESTARTS   AGE
calico-kube-controllers-75d56dfc47-pkkjj      1/1     Running   1          2d15h
calico-node-7sbx5                             1/1     Running   1          2d15h
calico-node-pcrxw                             1/1     Running   1          2d15h
calico-node-w8f9k                             1/1     Running   1          2d15h
coredns-66bff467f8-vldt2                      1/1     Running   1          2d15h
coredns-66bff467f8-vqz6v                      1/1     Running   1          2d15h
etcd-kmaster.example.com                      1/1     Running   1          2d15h
kube-apiserver-kmaster.example.com            1/1     Running   4          2d15h
kube-controller-manager-kmaster.example.com   1/1     Running   7          2d15h
kube-proxy-4kmkk                              1/1     Running   1          2d15h
kube-proxy-68b4r                              1/1     Running   1          2d15h
kube-proxy-8jg4r                              1/1     Running   1          2d15h
kube-scheduler-kmaster.example.com   
 ```
- In this scenario all pods are in the running status
  - This means that the pod has been bound to a nodes
  - All **container have been created**
  - **At least one container** is still running,or is starting/restarting
  - Other valid status are:
     - **Pending**: Pod has been accepted but is not running
       - Happens when the container image is still downloading
       - if the pods cannot be scheduled because of **resource constraints**, it'll also be in this status
   - **Succeeded**: All container within this pod have been **terminated successfully** and will not be restarted
     - **Failed**:All the containers within the pod have been **Terminated**, and at least one container returned a failure code
       - The failure codes is the exit code of the process when a container terminates
     - **Unknown**: The **state of the pod couldn't be determined**
       - A network error might have been occurred(for example the node where the pod is still running on is down)
- we can get the pod conditions using kubectl describe pod PODNAME
```
[vagrant@kmaster ~]$ kubectl describe pod kube-apiserver-kmaster.example.com -n kube-system
[...]
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
```
These are conditions which the pod has passed
- There are 5 different types of PodConditions:
  - **PodScheduled**: the pod has been scheduled to a node
  - **Ready**: Pod can serve requests and is going to be added to matching services
  - **Initalized**: the initialization containers have been started successfully
  - **Unschedulable**: the pod can't be scheduled (for example due to resource constraints)
  - **ContainersReady**: all containers in the pod are ready
- There is also a **Container** state:
```
[vagrant@kmaster ~]$ kubectl get  pod kube-apiserver-kmaster.example.com -n kube-system -o yaml
[...]
  containerStatuses:
  - containerID: docker://30ad807eb83cbafeb1a5ee5541b9d2be326525dc9b81819a49e7ccfe24d954b1
    image: k8s.gcr.io/kube-apiserver:v1.18.2
    imageID: docker-pullable://k8s.gcr.io/kube-apiserver@sha256:19a8020e4aaaa8bd41f5bca223e05183cfe66157393ef7a205720c49b2405e0f
    lastState:
      terminated:
        containerID: docker://581350dcb291c547f182d5c4592921aa3983a8b9c83519c6d367e5aee79d6bd0
        exitCode: 255
        finishedAt: "2020-05-22T16:28:01Z"
        reason: Error
        startedAt: "2020-05-20T13:40:42Z"
    name: kube-apiserver
    ready: true
    restartCount: 4
    started: true
    state:
      running:
        startedAt: "2020-05-22T16:28:12Z"
```
-  Container state can be running, Terminated , or waiting


