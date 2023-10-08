NOTE: This document contains base notes and has NOT been cleaned up at all yet.

---
# THEORY

---
# Practical
Install Prometheus using helm
1. if helm isnt installed run `brew install helm`
2. run `helm repo add prometheus-community https://prometheus-community.github.io/helm-charts`
3. always run `helm repo update`
4. install prometheus controller and required configs like config map etc. `helm install prometheus prometheus-community/prometheus`


If you run `kubectl get pods` you will get:
```
NAME                                                 READY   STATUS    RESTARTS   AGE
prometheus-alertmanager-0                            1/1     Running   0          112s
prometheus-kube-state-metrics-5b74ccb6b4-hbvjr       1/1     Running   0          112s
prometheus-prometheus-node-exporter-mkpm9            1/1     Running   0          112s
prometheus-prometheus-pushgateway-79ff799669-lrq74   1/1     Running   0          112s
prometheus-server-745d64557-kvbr2                    2/2     Running   0          112s

```
what the heck si kube state metrics?
- kubernetes api server exposes some metrics about the api server and the default installation on the kubernetes cluster. ksm controller, you can call it at the metrics endpoint and get a bunch MORE information, as in more than the API exposes.

We want to expose the prometheus server!!!
1. convert prometheus-server from clusterIP to nodeport by running `kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext`
2. Because you are on a mac with darwin you have to tunnel now... get the service name by using `kubectl get svc`, and run `minikube service prometheus-server-ext` and it will start the tunnel for you.

---

# Useful Links
