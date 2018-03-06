if your application is stateless you can horizontally scale it

-stateless = your application doesn't have a state,it doesn't write any local files/keep local sesions 

- all traditional databases(Mysql,postgres) are stateful,they have database files that can't be split over multiple instances

most web application can be made stateless
-session management needs to be done outside the container. 
-any files that needs to saved can't be saved locally on the container


scalling 

-scaling in kubernetes can be done using the replication controller
-the replication controller will ensuer a specified number of pod replicas will run at all time

-a pod created with the replica controller will automatically be replaced if they fail,get deleted, or are terminated
-using the replication controller is also recommended if you just want to make sure 1 pod is alwalys running, even after reboots

--you can the run a replication controller with just 1 replica 
--this makes sure that the pod is alwalys running 

---------------------

Replication set
-replica set is the next-getn replication controller

it supports a new selector that can do selection based on filtering according a set of values
--eg: 'environments' either 'dev' or "qa"
--not only based on equality, like the replication controller

eg: 'environment' == 'dev'

-this replica set, rather than the replication controller, is used by the deployment object



-a deployments declaration in kubernetes allows you to do app deployments and update
-when using the deployment object,you define the state of your application
--kubernetes will then make sure the clusters matches your desired state
-just using the replcation contoroller or 'replication set' might be cumbersome to deploy apps
--the deployment object is easier to use and gives you more possibilities


deployments

-with a deployment object you can 
--create a deployments(eg: deploying on app)

--update a deployment(eg: deploying a new verison)
--Do rolling updates (eg:zero downtime deployments)
--rollback to previous version
--pause/Resume a deployment (eg: to roll-out to only a certain percentage)


useful commands:


kubectl get deployments ---- get information on current deployments

kubectl get rs ---- get information about the replica set

kubectl get pods --show labels --get pods,and also show labels attached to, those pods
kubectl rollout status deployments/helloworld-deployment  ---get deployment status


kubectl set image deployment/helloworld-deployment k8s-demo=k8s-demo:2 ------run k8s-demo with image labe verion 2


kubectl edit deployment/helloworld-deployment   ---edit the deployment object

kubectl rollout status deployment/helloworld-deployment --get the status of the rollout

kubectl rollout history deployment/helloworld-deployment --get the history of the rollout

kubectl rollout undo deployment/helloworld-deployment  -- roll back to previous version
kubectl rollout undo deployment/helloworld-deployment --to-revision=n  ---rollback to any version 


----------------------
services 

-pods are very `dynamic`, they come and go on the kubernetes cluster
--when using a replicaion controller, pods are terminated and created during scaling operaions

--when using deployments, when updating the image verion,pods are terminated and new pod take the place of older pods

-that's why pods should never be accessed directly, but alwalys through a service

-service is the logical bridge between the 'mortal' pods and other services to end=users


services:

-when using the "kubectl expose" commnd ,created a new service for your pod, so it could be accessed externally
-creating a service will create an endpoint for your pods:

--a ClusterIP:a virtual IP address only reachable from within the cluster (this is the defalut)
--a Nodeport: a port that is the same on each node that is also reachable externally
--a LoadBalancer : a loadBalancer created by the cloud provider that will route external traffic to every node on the Nodeport(ELB on AWS) 


services:

-the options just show only to create virtualIP's or ports
-there is also possiblility to use DNS names
--ExternalName can provide a DNS name for the services
--eg:for services discovery using DNS

--this only works when the DNS add-on is enabled 

Labels

-Labels are key/value pair that can be attached to objects
--labels are like tag in AWS or other cloud providers, used to tag resources

-you can label your object, for instance your pod,following organizaiton structural

--key:environment-value: dev/dev/staging/qa/prod
--key:department-value:engineering/finance/marketing



labels are not unique and multiple labels can be added to one object

once labels are attached to an object,you can use filters to narrow down results
--this is called label selectors

-using labels selectors, you can use matching expressions to match labels

--for instance, a particular pod can only run on a node labeled with "environment" equals "development"
--more complex matching "environment" in "developments" or "qa"


Node Labels

-- you can also use labels to tag nodes

--once nodes are tagged, you can use label selectors to let pods only run on specific nodes

--there are 2 steps required to run a pod on a specific set of nodes:

--First you tag the node
--then you add a nodeSelector to your pod configuration.


Secrets

-secrets provides a way in kubernetes to distribute credentials,keys,password or "secret" data to pods

-kubernetes itself uses this secrets machanism to provide the credentials to access the internal API

-you can also use the same mechanism to provide secrets to your applicaion
-secrets is one way to provide secrets,native to kubernetes
--there are still other ways yout container can get its secrets if you don't want to use secrets(eg: use an external valt srevice in yout app)

secrets:

secrets can be used in the following ways:

--use secrects as environment variables
--use secrets as a file in a pod
 ---this setup uses volumes to be mounted in a container
 ---in this volume you have files
 ---can be used for instance for dotenv files or your app can just read this file

 -use an external image to pull secrets(from a private image registry)


 -secret can also be an ssh key or an ssl certificate.






