NOTE: This document contains base notes and has NOT been cleaned up at all yet.


Deployment —> USE THIS NOT POD

adds another layer on top of pods! the manifest can say things such as ho wmany replicas you want and so the deployment will make sure there is a pod with w.e you need

it will od auto scale and auto control

it uses replica set controller —> controllers are needed to check that states are the same!

example replica set controller makes sure what our manifes says replicas should be are actually what it is.

Deployment vs replica set?

replica set —> is a controller that implements auto healing by checking against yaml manifest

deployment —> if you create deployment replica set is automatically created.

`kubectl get all` —> gets all stuff in your namespace

`kubectl get all -A` —> gets all for all namespaces

`kubectl get pods -w` —> lets you watch the status of hte pods live

 you update something in the manifest and want to apply the updates without shutting down your current shit you do kubectl apply -f <manifest>.yml
