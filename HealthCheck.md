# Health Checks
------
 - if your application **malfunctions**, the pod and container can still be running, but the application might not work anymore
 - To **detect** and **resolve** problems with your application, you can run **health checks** 
 - you can run 2 different types of Health Checks
   - Running a **command** in the container **periodically** 
   - periodic checks on a **URL**(HTTP)
 - The typical production appication behind a load balancer should alwalys have **health checks** implemneted in some way to ensure **availability** and **resiliency** of the app
 
 ### examples
 healthcheck.yml
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
        livenessProbe:
          httpGet:
            path: /
            port: nodejs-port
          initialDelaySeconds: 15
          timeoutSeconds: 30
 ```
