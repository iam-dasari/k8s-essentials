What is kubernetes?
----------------------
 - Kubernetes is a container orchestration tool to automate deployments
 - image--> physical file
 - container-->running instance of image with some config
 - we give kubernetes to take charge of running the images as orchestrator

Steps:
----------
 - Create Dockerfile and build image
 - Push to container registry (like Docker Hub)
 - Write manifests to run the images (docker run is the command to run images in Docker)

Docker Swarm vs Kubernetes
------------------------------
 - Networking and storage solutions are better in kubernetes

Namespaces
------------
 - Namespaces are isolated project space for kubernetes resources. If no namespace is provided then kubernetes use default namespace
 - kubectl get namespaces or kubectl get ns
 - kubectl apply -f 01-namespace.yaml
 - kubectl create vs apply --> When resource doesn't exist use create otherwise you will get error.
   Where as apply it can be used at any time.
 - kubectl delete -f 01-namespace.yaml 
 - kubectl api-resources

Pods
------
 Pods are smallest deployment unit in K8
 Pod vs container
 ------------------
  - 1 pod can have multiple containers
  - all containers inside pod share same storage and n/w
  - kubectl exec -it simple-pod -n roboshop -- bash
  - kubectl get pods -n roboshop
  - multi-containers: 1. side car patterns, 2. proxy patterns and 3. init containers
    kubectl exec -it multi-container -c sidecar -- bash (it will access nginx container details)
 labels
 --------
  - labels are used in selectors, it has some functional adantage apart from filtering
  - kubectl describe pod <pod-name>
 labels vs annotations
 ------------------------
  - labels can't have special characters in key names but annotations can have
  - labels key have some length restrictions but annotations length can be more than labels
  - labels are used in kubernetes resources selectors, annotations are used in selecting external resources

VM and Docker
---------------
 - Resource utilization - can dynamically consume resources (not blocking system resources)
      App locks - can consume more memory because of code defect, so container can block complete system resources, we can implement resources to avoid this disadvantage
      1 cpu = 1000m, 250m=0.25 cpu

imagePullPolicy
-----------------
 Developer did some change, he pushed new image to docker. We run pod again like kubectl apply -f <file-name>
 Already pulled image: default
 imagePullPolicy: always (we no need to run kubectl apply again and again otherwise kubernetes will run older version)

 Environment variables
 ----------------------------
  env:
  - name: USERNAME
    value: "Pavan"
  - name: PLACE
    value: "Guntur"
 kubectl exec -it env-demo -- bash
 # env

 ConfigMap
 ------------
  - Keep the config away from container
   kubectl get configmaps
   kubectl describe configmap course-config
 Attach to pod
 --------------
   valueFrom:
        configMapKeyRef:
          name: course-config
          key: COURSE
 kubectl exec -it config-pod -- bash
 # env

 Advantage: I don't need to change pod manifest instead just update the values in ConfigMap and restart the pod
 Refer full configmap: 
   envFrom:
   - configMapRef:
       name: course-config

Secrets
--------
 - Secrets are used for usernames and passwords, tokens ect.,
   - echo "Pavan" | base64
   - echo "UGF2YW4K" | base64 --decode

Services
----------------
 - Services are used to expose applications to outside world
 - To balance the load - deployment & replicaset
  1. ClusterIP - Within cluster
  2. NodePort - For Dev Environment
  3. LoadBalancer - Used for cloud
 - kubectl get service or kubectl get svc
 - Login to one pod and use curl <ip-address> or curl <name-of-service> 
 - When we use name-of-service it is called service mesh as ip addresses keep on changing