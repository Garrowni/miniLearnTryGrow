NOTE: This document contains base notes and has NOT been cleaned up at all yet.

---
# THEORY

---
# Practical
Install Grafana using helm
1. if helm isnt installed run `brew install helm`
2. add grafana helm chat `helm repo add grafana https://grafana.github.io/helm-charts`
3. run `helm repo update`
4. run `helm install grafana grafana/grafana`
5. rn `kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo`
6. switch to NodePort `kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-ext`
7. because your on mac run `minikube service grafana`

Add prometheus as a data source
1. click add data source
2. pick prometheus
3. use the ip thats not the tunnel... the one that has the <minikubeip>.<portnumber>

Import a prometheus dashboard!
1. go to dashboards
2. in the drop down select import
3. enter `3662`
4. in the bottom drop down pick your prometheus data source
5.  press import! boom theres a dashboard

---

# Useful Links
 