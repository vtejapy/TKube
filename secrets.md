# Secrets
----------------
 - secrets provides a way in kubernetes to distribute **credentials**,**keys**,**password** or "**secret"** data to pods
 - kubernetes itself uses this secrets machanism to provide the credentials to access the internal API
 - you can also use the **same mechanism** to provide secrets to your applicaion
 - secrets is one way to provide secrets,native to kubernetes
   - there are still **other ways** yout container can get its secrets if you don't want to use secrets(eg: use an **external valt srevice** in yout app)

 - secrets can be used in the following ways:
    - use secrects as **environment variables**
    - use secrets **as a file** in a pod
    - this setup uses **volumes** to be mounted in a container
    - in this volume you have **files**
    - can be used for instance for **dotenv** files or your app can just read this file

 - use an external image to pull secrets(from a private image registry)


 - secret can also be an ssh key or an ssl certificate.
