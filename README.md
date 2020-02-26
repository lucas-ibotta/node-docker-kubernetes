# Get this simple app running, with Docker and Kubernetes

Follow setup directions for Minikube [here](https://kubernetes.io/docs/tutorials/stateless-application/hello-minikube/)

To run this app normally, we would just use:

`node server.js` and check `http://localhost:8080/`

To run it in an extremely overpowered hello world Kubernetes cluster:

# Build Docker Image & Deploy
1. `minikube start --vm-driver=xhyve` - start minikube locally
2. `docker build -t hello-node:v1 .` - build a Node docker image with a v1 tag
3. `docker run --expose 8080 -p 8080:8080 -it hello-node:v1` - run locally

# Get it going on Kubernetes
1. `kubectl run hello-node --image=hello-node:v1 --port=8080` - create a deployment which manages a pod
2. `kubectl get deployments` and `kubectl get pods` - check on your deployment and pods

# Expose this App outside Kubernetes network
1. `kubectl expose deployment hello-node --type=LoadBalancer` - create service outside Kubernetes virtual network
2. `kubectl get services` - see your service deployment
3. `minikube service hello-node` - run the service with minikube

# Update Your App
1. Edit `server.js`
2. `docker build -t hello-node:v2 .` - build the next docker image with `v2` tag
3. `kubectl set image deployment/hello-node hello-node=hello-node:v2` - set new image on the deployment
4. `minikube service hello-node` - run the new version of your service

# Scale Your App
1. `kubectl scale deployments/hello-node --replicas=4`
2. `kubectl get deployments`

# Delete Your Work
1. `kubectl delete service hello-node` & `kubectl delete deployment hello-node`
2. `minikube stop`
