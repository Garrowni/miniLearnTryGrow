NOTE: This document contains base notes and has NOT been cleaned up at all yet.
control plane

---

- api server
    - exposes k8s
    - takes all the requests from external stuff
- etcd
    - backing storage of entire cluster
    - key value pairs aka objects
    - stores state of cluster
- scheduler
    - in charge of scheduling the work onto pods
    - finds out the pod from the api server and tells the specific pod
- CM - controller manager
    - makes sure all the controllers are working properly/running
    - ex controller —> replicaset controller —> in charge of k8s pods and making sure there are as many replicas as there should be
- ccm - cloud controller manager


Worker Node / Data Plane
Data plane/Worker Node components

- kubelet
    - responsible for the pod (make sure its always running)
    - if its not running it tells kubernetes HEY DO SOMETHING!
- kube-proxy
    - provides networking
    - provides ip addresses
    - provides load balancing
- container runtime
    - actually RUNS the container
    - containerd
    - cri-dockerd]



--- 

Container 
- docker
- has image
    - app
    - dependencies
    - image build instricturions
    - use docker run xxxxxxx
- on kubernetes you don't deploy containers, you deploy pods.

Pod
- wrap around containers
- takes yaml manifest (adds ease, replaces docker run)
    - image
    - ports
    - volumes
    - etc…
- runs spec of docker image and can make it a container
- can make multiple in side (a pod could have multiple containers)
    - containers share network and storage
---
# Useful Links
[k8.io/pods](https://kubernetes.io/docs/concepts/workloads/pods/)