Flow
---------
 1. Develop Dockerfiles and manifest files
 2. Build the images
 3. Push to container registry
 4. Run manifest files

 mongodb
 -----------
  - Create namespace (kubectl apply -f 01-namespace.yaml)
  - verify namespace is created or not (kubectl get ns)
  - Build image (docker build -t dasaridevops/mongodb:1.0.0 .)
  - Login to docker (docker login registry-name)
  - You can logout and login again with proper docker account details
  - Push the built images (docker push dasaridevops/mongodb:1.0.0)

  Faced ImagePullBackOff error
  -------------------------------
   - create a secret with docker credentials
   - kubectl create secret docker-registry my-registry-secret --namespace roboshop \
        --docker-server=docker.io \
        --docker-username=username \
        --docker-password=password \
        --docker-email=email-id
    - Verify if secret created or not - kubectl get secrets
    - Use  imagePullSecrets:
            - name: my-registry-secret
     in the manifest file

  catalogue
  ----------
   - move MONGO=TRUE & MONGO_URL environment variable to ConfigMap
   - kubens roboshop
  
  web
  -------
   - when you provision user, you change nginx conf and include user reverse proxy
   - push changes to git
   - do docker build
   - restart the container
   - But docker build is a heavy process. Recommendation is, when the code is changed then only go for build, if config changed, you should not go for image build, you should restart
   - we can keep config files also in configmap and remove configuration from roboshop.conf file
