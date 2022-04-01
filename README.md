# Deploy a React app to Kubernetes using Docker  

[Source (LogRocker)](https://blog.logrocket.com/deploy-react-app-kubernetes-using-docker/)  

```
mkdir react-docker-kubernetes
cd react-docker-kubernetes
mkdir K8s 
npx create-react-app react-docker
npm run build
# create Dockfile in app folder root
docker build -t your_docker_username/react-docker .
docker run -d -p 3000:80 your_docker_username/react-docker
docker stop $(docker ps -a -q)

minikube start
kubectl create namespace react-docker
kubectl config set-context --current --namespace=react-docker
# create deployment.yml
kubectl apply -f deployment.yaml
kubectl get deployment -w

# create load-balancer.yml
kubectl apply -f load-balancer.yaml
kubectl get services -w
http://your_minikube_ip:31000
minikube ip
kubectl scale deployment react-docker --replicas=10
kubectl get deployment -w
kubectl scale deployment react-docker --replicas=3
```