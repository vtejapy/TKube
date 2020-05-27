# Deployments
---------------------
 - A deployments declaration in kubernetes allows you to do app **deployments** and **update**
 - when using the deployment object,you define the **state** of your application
   - kubernetes will then make sure the clusters matches your **desired** state
 - just using the **replcation contoroller** or **replication set** might be **cumbersome** to deploy apps
   - the **deployment object** is easier to use and gives you more possibilities
 - with a deployment object you can 
    - **create** a deployments(eg: deploying on app)
    - **update** a deployment(eg: deploying a new verison)
    - Do **rolling updates** (eg:zero downtime deployments)
    - **rollback** to previous version
    - **pause/Resume** a deployment (eg: to roll-out to only a certain percentage)


### useful commands:


`kubectl get deployments ---- get information on current deployments`

`kubectl get rs ---- get information about the replica set`

`kubectl get pods --show labels --get pods,and also show labels attached to, those pods`
`kubectl rollout status deployments/helloworld-deployment  ---get deployment status`


`kubectl set image deployment/helloworld-deployment k8s-demo=k8s-demo:2 ------run k8s-demo with image labe verion 2`


`kubectl edit deployment/helloworld-deployment   ---edit the deployment object`

`kubectl rollout status deployment/helloworld-deployment --get the status of the rollout`

`kubectl rollout history deployment/helloworld-deployment --get the history of the rollout`

`kubectl rollout undo deployment/helloworld-deployment  -- roll back to previous version`
`kubectl rollout undo deployment/helloworld-deployment --to-revision=n  ---rollback to any version` 

### Example
deployments.yml
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: helloworld-deployment
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: helloworld
    spec:
      containers:
      - name: k8s-demo
        image: wardviaene/k8s-demo
        ports:
        - name: nodejs-port
          containerPort: 3000
```
