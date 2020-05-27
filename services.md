
# services
----------------------
 - **pods** are very **dynamic**, they come and go on the kubernetes cluster
   - when using a **replicaion controller**, pods are **terminated** and created during scaling operaions
   - when using **deployments**, when **updating** the image verion,pods are **terminated** and new pod take the place of older pods

 - that's why pods should never be accessed directly, but alwalys through a **service**

 - service is the **logical bridge** between the `mortal` pods and other **services** to **end=users"
- when using the "kubectl expose" commnd ,created a new service for your pod, so it could be accessed externally
 - creating a service will create an endpoint for your pods:

   - a **ClusterIP**:a virtual IP address only reachable from within the cluster (this is the defalut)
   - a **Nodeport**: a port that is the same on each node that is also reachable externally
   - a **LoadBalancer** : a loadBalancer created by the **cloud provider** that will route external traffic to every node on the Nodeport(ELB on AWS) 
 - the options just show only to create **virtualIP's** or **ports**
 - there is also possiblility to use **DNS names**
   - **ExternalName** can provide a DNS name for the services
   - eg:for services discovery using DNS
   - this only works when the **DNS add-on** is enabled 
  ### example
  helloworld-nodeport-service.yml
  
  ```
  apiVersion: v1
kind: Service
metadata:
  name: helloworld-service
spec:
  ports:
  - port: 31001
    nodePort: 31001
    targetPort: nodejs-port
    protocol: TCP
  selector:
    app: helloworld
  type: NodePort
  ```
  -  Note: by default services can only run between ports 30000-32767, but you could change this behavior by adding the --serveces-node-port-range=argument to he kube-apiserver
