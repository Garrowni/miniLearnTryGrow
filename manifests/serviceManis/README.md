NOTE: This document contains base notes and has NOT been cleaned up at all yet.

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






