
# Labels
----------------------

  - Labels are key/value pair that can be attached to objects
    - labels are like **tag** in AWS or other cloud providers, used to tag resources

  - you can **label** your **object**, for instance your pod,following organizaiton structural

    - **key**:environment-**value**: dev/dev/staging/qa/prod 
     - **key**:department-**value**:engineering/finance/marketing
  - labels are **not unique** and **multiple** labels can be added to one object
  - once labels are attached to an object,you can use filters to narrow down results
    - this is called **label selectors**

  - using labels selectors, you can use **matching expressions** to match labels

    - for instance, a particular pod can only run on a node labeled with "environment" equals "development"
    - more complex matching "environment" in "developments" or "qa"
## Node Labels
   - you can also use labels to tag nodes
   - once nodes are tagged, you can use label selectors to let pods only run on specific nodes
   - there are 2 steps required to run a pod on a specific set of nodes:

     - First you tag the node
     - then you add a nodeSelector to your pod configuration.
