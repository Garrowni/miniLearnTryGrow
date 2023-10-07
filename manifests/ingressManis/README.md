NOTE: This document contains base notes and has NOT been cleaned up at all yet.

---

----What is ingress?  why is it required???----
service gives --> service discovery
              --> load balancing
              --> exposed 
BUT load balancing is very basic round robin... with VMs LBs were way more awesome

SO in comes ingress!

---
1. Choose load balancer type you want.... Use nginx as this example, but it would depend on what you need it to do... host based, tls, path based,etc...
2. . you deploy nginx onto cluster yourself
3. you set up ingress to use nginx
---

# practical integration

## Host based
1. Create a yaml for the ingress type. for example ingress-wildcard-host.yml
2. create ingress controller (google kubernetes nginx ingress controller minikube in this case.) 
3. Wow for this case its super easy! run `,inikube addons enable ingress`
4. test that the controller is running `kubectl get pods -n ingress-nginx`
5. now apply your ingress yaml `kubectl apply -f ingress-wildcard-host.yaml`
6. now run `kubectl get pods -A | grep nginx`
7. use hte namespace and pod name to check logs and make sure its found the ingress
`kubectl logs ingress-nginx-controller-7799c6795f-f4g4r -n ingress-nginx`
the bottom line should have something like this " 7 event.go:285] Event(v1.ObjectReference{Kind:"Ingress", Namespace:"default", Name:"ingress-wildcard-host-example", UID:"79a815a6-8cb6-48c5-80f1-ec174d80e70c", APIVersion:"networking.k8s.io/v1", ResourceVersion:"65023", FieldPath:""}): type: 'Normal' reason: 'Sync' Scheduled for sync"

8. (IF ON LAPTOP) update `/etc/hosts`
you have to map your host to address. host + address can be found using `kubectl get ingress`




NOTE: current settings on this laptop prevent me from actually being able to try this further.


---
# Useful Links
[k8.io/ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
[k8.io/ingress-controllers](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers)
