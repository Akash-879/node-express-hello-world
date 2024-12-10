# Node Js CICD application
Run it on Local machine

![localhost:3000](/public/images/localhost_3000.png?raw=true "Node & Express")

# Step 1: Git clone
```
  git clone https://github.com/eMahtab/node-express-hello-world
  cd node-express-hello-world
  npm install
  npm start

  Go to localhost:3000
```  
# Step 2: Build Dockerfile & Run container
```
   # docker build -t <tag-name> .
   # docker run -d -p 3001:3001 <image-name>
   # docker push tag <image-tag> <repo/image>  #pushed image to docker hub
```
# Step 3: Kubernetes Deployments using Minikube Cluster
```
   # minikube start
   # kubectl apply -f k8s/deployment.yml
   # kubectl apply -f k8s/service.yml
   # kubectl get deployments   #check deployments are ready in state
   # minikube service <service-name>  #get the nodeport ip 
```
# Step 4: Jenkinsfile
```
  # Install & run jenkins server
  # Create pipeline
  # add required plugin (eg.Docker,git,pipeline etc
  # Configured secrets (eg.docker-cred,git-cred etc)
  # chose from pipeline script from scm
  # build pipeline
```
 
   
