NOTE: This document contains base notes and has NOT been cleaned up at all yet.

---

Default types in the YAML:
1. Cluster IP --> only communicate inside k8, you would get discovery and load balancing
2. Nodeport --> allows access inside organization/network(have access to your nodes or vpc)  (people with access to worker node ips), 
3. LoadBalancer --> exposes to external world
      --> by default will only work on cloud
      --> need ingress if your gonna do local(will discuss later)
 

------
Advantages
--> service descovery
--> load balancing
--> expose (available to world, available to org)
-----

SERVICES

if there is no services...
Say we have 3 pods all with application ip addresses
pod 1: ip 172.15.3.4
pod 2: ip 172.15.3.5
pod 3: ip 172.15.3.6

pod 1 dies.....

replicacontroller goes heck no there cant be 2... manifest says 3!
pod 1 is replaced....
WOW autohealing (which is here beacuse of replica sets) is awesome!
but uh oh now its a new issue..... the ip address of the new pod is wrong!

pod 1: ip 172.15.3.7
pod 2: ip 172.15.3.5
pod 3: ip 172.15.3.6


Now any users that were working on pod 1 ip 172.15.3.4 cant communicate anymore!!!!
To solve this problem kubernetes has "Kubernetes service"


Service aka SVC
goes ontop/outside of the pods
load balancing.
 service discovery, so if one of those ips goes away it knows the new ones
          --> uses labels and selectors (since ips can change they dont use that)
              --> for every pod created theres a label in metadata 

 example:
 deployment --> manifest with 3 replicas of a payments container with "payments" label

 replicaset is gonna make:
 payments pod 1: ip 172.154.3.4 with label payments
 payments pod 2: ip 172.154.3.5 with label payments
 payments pod 3: ip 172.154.3.6 with label payments

pod 2 dies???
replicaset replaces that pod... but manifest said to give it label payments...
payments pod 1: ip 172.154.3.4 with label payments
payments pod 2: ip 172.154.3.9 with label payments
payments pod 3: ip 172.154.3.6 with label payments

we have services on so users are ONLY connecting through SVC payments.
SVC can see 3 pods still all labeled payments. no change :)

SVC --> load balancing
    --> service discovery
    --> expose to world


------------------
Reminder: for this app its on 8080/demo
so... using cluster port
1. minikube ssh
2. curl -L http://xxx.xxx.xxx.xxx:8000/demo 

using node port
1. curl -L


# Useful Links
[k8.io/services](https://kubernetes.io/docs/concepts/services-networking/service/)