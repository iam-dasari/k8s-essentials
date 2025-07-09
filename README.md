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
 - Namespaces are isolated project space for kubernetes resources
 - kubectl get namespaces or kubectl get ns
 - kubectl apply -f 01-namespace.yaml
 - kubectl create vs apply --> When resource doesn't exist use create otherwise you will get error.
   Where as apply it can be used at any time.
 - kubectl delete -f 01-namespace.yaml 
 - kubectl api-resources