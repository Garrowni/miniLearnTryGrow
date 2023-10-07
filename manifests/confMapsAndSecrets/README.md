NOTE: This document contains base notes and has NOT been cleaned up at all yet.

---
What is the difference between a config map and a secret?
They both store data that your pod/app/deployments can access at a later time....
How are they different?
config map is for non-senesative data
Secrets are for sensitive data!

# What is a ConfigMap?
data will go right into etcd.

1. you make a config map (yaml file)
    - put all the details you need from k8 docs
2. use kubectl to apply the config map on the cluster
3. config map is created, at the same time API server saves this info in etcd.

If hacker is trying to steal your stuff and has gained access to you k8 cluster he could go run describe config map and get the info in it. He could alsso go to etcd and do the same.


# What is a Secret  
- Any kind of data put in secret will be encrypted "in Rest" before going into etcd
- RBAC --> you could say only devops gets access to srets
- You can also use a custom encryption
- whenever using secrets you should have very strong RBAC (use least privilege like with IAM!)


---


# Useful Links
[k8.io/configMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
[k8.io/secrets](https://kubernetes.io/docs/concepts/configuration/secret/)