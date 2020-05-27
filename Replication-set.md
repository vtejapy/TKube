# Replication set
---------------------
 - **Replica** set is the next-getn replication controller

 - it supports a new selector that can do selection based on **filtering** according a **set of values**
   - eg: 'environments' either 'dev' or "qa"
   - not only based on equality, like the replication controller

     - eg: 'environment' == 'dev'

  - this **replica set**, rather than the replication controller, is used by the deployment object
