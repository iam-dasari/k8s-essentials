
ReplicaSet
-------------
 - Pod is subset of ReplicaSet
 - ReplicaSet internally creates pod only
 - kubectl get rs
 - Replicaset will maintain only no of replicas that is pods but if any code changes that will not be reflected
 - To make application changes, we need Deployment

 Deployment
 ------------
  - Deployment is same as ReplicaSet but it is meant for applications running and changes will get reflected
  - Pod is subset of ReplicaSet and ReplicaSet is subset of Deployment
  - kubectl get deployments
  - we can update applications to next version in zero downtime