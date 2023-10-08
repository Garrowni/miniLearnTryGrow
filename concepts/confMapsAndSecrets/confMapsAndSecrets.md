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

# Practicals

## Config Map

### Using it as ENV vars ###
DONT DO THIS!
Why? because you cant change an env var in a container without restarting the container....
WHY IS THAT BAD?! because traffic loss!!!!
What do you use instead??? Volume Mounts!
(SEE NEXT SECTION)
1. Create a config map called `cm.yml`
2. put an extremely basic config in there. For example
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: test-cm
data:
  db-port: "3306"

```
3. run `kubectl apply -f cm.yml` --> apply the config map
4. run `kubectl get cm` --> get a list of config maps
5. run `kubectl describe cm test-cm` --> get details of the cm
6. go back into your deployment config (deployment.yml)
7. in container spec add a block to get the env var
```
      containers:
      - name: python-app
        image: ngarrow/python-app:latest
        env:
          - name: DB-PORT #what your going to use to call it
            valueFrom:
              configMapKeyRef:   
                name: test-cm #name you gave the config map
                key: db-port  # key thats in data in the config map
        ports:
        - containerPort: 8000
```
8. run `kubectl apply -f deploy.yaml` --> apply the change
9. run `kubectl exec -it sample-python-app-<podstuff> -- /bin/bash`
10. from in the node run `env | grep -i db` --> this will output the env var yay!

---
## Volume Mount
volumes are storage. you create the storage and then let the pod read it.
1. go into `deployment.yaml`
2. add a volume which reads from a configMap. the name will be the name for your volume under config map name will need to match the name in your cm.yml

``` 
      volumes: 
        - name: db-connection
          configMap:
            name: test-cm

```

3. under containers add a volume mount. name should match the volume. mountPath is where you want to mount it on the pod.

4. run `kubectl exec -it sample-python-app-<podstuff> -- /bin/bash`

5. run `cat /opt/db-port` | more --> it should output your port


6. exit ssh! now if you want to go ahead and change it.... go back into your cm.yml and make your changes saving them. 
(appears to be optional)

7. run `kubectl apply -f <cm name>` apply your change

8. run `kubectl describe cm <cm name>` This should show your change 

9. run `kubectl exec -it sample-python-app-<podstuff> -- /bin/bash`

10. run `cat /opt/db-port` | more --> it should output your updated port

---

### Make a secret through cli rom literal
1. run `kubectl create secret generic test-secret --from-literal=db-port-secret="3333"`

2. if you run kubectl describe secrets test-secret you will see that you... cant see the value!

Interesting --> decrypt basic k8 encryption
1. run `kubectl edit secret test-secret`
2. copy the encrypted value
3. run `echo <encryptedvalue> | base64 --decode`

Thats part of why it would be good to add additional encryption.  

you could use something like hashicorp vault or "sealed secrets" but it will you require to pass it to the API server.

4. in deplyment.yaml add a volume
```
      volumes: 
        - name: db-connection
          configMap:
            name: test-cm
        - name: db-secret-volume
          secret:
            secretName: test-secret
```
5. in deployment.yaml add a volume mount
```
          - name: db-secret-volume
            readOnly: true
            mountPath: "/etc/secret-volume"
```
6. apply the deployment.yml
7. ssh onto a pod
8. run `cat /etc/secret-volume/db-port-secret`
---
# Useful Links
[k8.io/configMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
[k8.io/secrets](https://kubernetes.io/docs/concepts/configuration/secret/)