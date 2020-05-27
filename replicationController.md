# scaling
 * if your application is **stateless** you can horizontally scale it
   * stateless = your application doesn't have a **state**,it doesn't **write** any **local files**/keep local sesions 
   - all traditional databases(Mysql,postgres) are **stateful**,they have database files that can't be split over multiple instances

 * most **web application** can be made stateless
   - **session management** needs to be done outside the container. 
   - any files that needs to saved **can't be saved locally** on the container


- scaling in kubernetes can be done using the **replication controller**
- the replication controller will **ensuer** a specified number of **pod replicas** will run at all time

- a pod created with the replica controller will **automatically** be **replaced** if they fail,get deleted, or are terminated
- using the replication controller is also **recommended** if you just want to make sure **1 pod** is alwalys running, even after reboots
  - you can the run a replication controller with just **1 replica** 
  - this makes sure that the pod is alwalys running
