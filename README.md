# miniLearnTryGrow
Learn containers!


---

Important General Knowledge

---------Main Differences Between Docker and Kubernetes--------
Docker = container platform
K8s = container orechstration --> allows you to build your docker image and offers auto healing. auto scaling, clustering, load balancing, etc.


---------Main Differences Between Docker Swarm and Kubernetes--------
- dark swarm is only for simple aplications, simple and fast set up, support is more limited
- kubernetes is suitable for large orgs, offers more scalability, network capabilities policies, huge 3rd party ecosystem support


---------Docker container vs Kubernetes Pod---------
- docker container has the app itself packaged up and whatever is needed to run the appk
- kubernetes pod is defined using YAML (runtime spec) that lets you RUN 1 or more containers


---------What is a namespace in k8s?--------------
- its kind of like a project in AWS or GCP --> k8s = reviewly && workspaces = project1, project2
- lets you seperate workspaces, allow for multiple teams/projects without stomping on eachothers toes
- but its all the same cluster technically


--------day to day activities of DevOps eng on k8s--------------
- manage k8s clusters for org
- ensure apps are deployed and there are no issues with them
- monitoring is good
- no bugs
- maintenance activities
  - upgrade versions, installing default mandatory packages, security updates
- subject matter exports


---------Main Components of k8 Architecture--------

Control Plane (equates to all masternodes combined)
---------------------------------------------------
- API Server --> handle apis that talks to end users. 
- Scheduler --> schedules resources on the cluster
- Controller Manager (CM) --> manages the other controllers
- Cloud Controller Manager )CCM) --> has logic to spin up load balancers and stuff like that through cloud, basically how the cloud interfaces with k8s
- ETCD --> object store, all resources of k8s stored here as key value pairs


Data Plane (worker nodes)
----------------------------
- Kubelet --> responsible to manage the containers within the pod the kubelet is on
          --> manage containers scheduled to run on the pod
              --> ensures healthy and running
              --> ensures proper resources they need are available
         --> communicates iwth k8 API
              --> gets info about containers that SHOULD  be running on the node
              --> using this info it starts/stops containers as neeed
              --> restarts containers if need be
- Kube-Proxy --> networking, takes care of updating ip tables
            --> maintain network rules on each node
            --> updates roles dynamially as services added/removed
            --> client sends a request to a service, req intercepted by kubeproxy on node where it was received, kube-proxy llooks up destination endpoint for the service, routes request accordingly
            --> ensures services can communicate with eachother
- Container Runtime --> needed to run the actual container
                    --> ex/ containerd

----What are labels and selectors used for?------
- used by service to identify pods
    - even if a pod is deleted and a new pod is spun up the ip will change by label wont.

--------Different types of services in k8s---------
- cluster ip mode
    --> only exposed within cluster
    --> the cluster ip is only available within the cluster
- node port mode
    --> expose within network
    --> anyone in your org who has access to your node address
- load balance mode
    --> expose to the pubic
    --> by default can only be done on cloud

------More detail on difference between NodePort and LoadBalancer type service----
- node port --> kube-proxy updates IPTables with node ip address & port choesen in the service config to access the pods

- LB --> C-C-M creates external LB IP using underlying cloud provider login in the CCM and then users can access services using the external IPvb 

---
