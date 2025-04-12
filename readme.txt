i used windows os, dokcker desktop and minikube
petclinic-chart // folder helm chart in my project
minikube is local Kubernetes
kubectl get services//show the services
kubectl get svc petclinic//You're asking Kubernetes to show details about a specific service named petclinic
NAME        TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
petclinic   NodePort   10.111.44.46   <none>        80:30685/TCP   22h
Check Pod Events:
kubectl describe pod <pod-name> 
The step in project:
1-Clone the code from github repository ->git clone https://github.com/spring-projects/spring-petclinic.git
2-Raed the instructions from Readme file I opened the current directory in visual code
3-Run command ./mvnw package
4-I tried to execute the command java -jar target/*.jar, but it is not working. I tried java -jar target/spring-petclinic-3.4.0-SNAPSHOT.jar, and it is working
5-I checked It is run in localhost:8080
6-Install minikube 
7-minikube start
8-docker build -t dsyer/petclinic -f .devcontainer/Dockerfile . //in petclinic.yml spec container image dsyer/petclinic build dockerfile
9-docker run --name workload -d -p 8080:8080 dsyer/petclinic //create container name workload
10-docker compose up postgres//run postgres service
11-kubectl apply -f k8s/petclinic.yml //deployment
12-kubectl apply -f k8s/db.yml
minikube service demo-db
13-minikube service petclinic  //run service selector: app;petclinic
14-db.yaml create //kind: StatefulSet
application-postgres.properties// show the environment postgresql
kubectl get statefulset // show the statefulset deploy
kubectl get pods//show the pods
kubectl exec -it demo-db-0 -- env//show environment inside pod
kubectl logs podname //logs
kubectl describe pod podname
check database is connection use kubectl logs podname
15-install helm->choco install kubernetes-helm
16-helm create petclinic-chart
17-helm install or upgrade petclinic-release ./petclinic-chart
18-create ingress file
ingress steps:
enable ingress in minikube
minikube addons enable ingress
kubectl port-forward svc/petclinic 80:80
1-minikube start --addons=ingress
2-create petclininc-ingress.yaml
3-C:\Windows\System32\drivers\etc\hosts add 127.0.0.1 petclinic.local
install nginx 
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install nginx-ingress ingress-nginx/ingress-nginx --namespace kube-system
minikube tunnel // to run with ingress must be activate to run the app with kubernetes and ingress
minikube tunnel simulates that behavior by creating a route between your local machine and the LoadBalancer service, 
allowing you to access it using an external IP.
A LoadBalancer service in Kubernetes is a way to expose your application to the outside world through 
a single external IP address that automatically distributes traffic to the underlying pods.

sumrray:
i run the ./mvnw package to prepare jar file and after that i execute java -jar target/spring-petclinic-3.4.0-SNAPSHOT.jar
to run application spring boot in my local host port 8080
i add configuration in dockerfile to prepare spring boot application
WORKDIR /app->working directioy in docker
COPY . .->copy the context from my computer to working diretory in docker
RUN ./mvnw package->i run the commnad to prepare the jar file
EXPOSE 8080->is port spring boot application
CMD ["java", "-jar", "target/spring-petclinic-3.4.0-SNAPSHOT.jar"]->run spring boot application

i execute the command docker build -t dsyer/petclinic -f .devcontainer/Dockerfile . to create image with name
dsyer/petclini because this image name it is Kubernetes pulled
i execute the command docker compose up postgres//run postgres service to prepare the database postgress:17 with name
postgress because this image name it is Kubernetes pulled

execute the command install minikube to install minikube in my computer to use it local Kubernetes
execute the command minikube start to run Kubernetes
execute the command kubectl apply -f k8s/petclinic.yml to create petclinic service and deployment
execute the command kubectl apply -f k8s/db.yml to create demo-db service and deployment
execute the command minikube service demo-db to run service
execute the command minikube service petclinic  to run service 
selector: app;petclinic // name service 
add in db.yaml kind: StatefulSet to store database
i see in application-postgres.properties file the environment postgresql to add in env Environment Variable in petlininc.yml

execute the command kubectl get statefulset to show the statefulset deploy i check if statefulset deployed
execute the command kubectl get pods to show the pods and check if is running 
execute the command kubectl exec -it demo-db-0 -- env to see environment inside pod and ensure the environment variable is correct
execute the command kubectl logs podname to print logs and see where is the problem
execute the command kubectl describe pod podname to print information about the pod and see the process
check database is connection use kubectl logs podname
execute the command minikube start to run Kubernetes
execute the command choco install kubernetes-helm to install helm in my computer
helm create petclinic-chart to create helm chart
helm install or upgrade petclinic-release ./petclinic-chart to create the service
create ingress file
ingress steps:
enable ingress in minikube
minikube addons enable ingress
kubectl port-forward svc/petclinic 80:80
1-minikube start --addons=ingress
2-create petclininc-ingress.yaml
3-C:\Windows\System32\drivers\etc\hosts add 127.0.0.1 petclinic.local
install nginx 
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install nginx-ingress ingress-nginx/ingress-nginx --namespace kube-system
minikube tunnel // to run with ingress must be activate to run the app with kubernetes and ingress
minikube tunnel simulates that behavior by creating a route between your local machine and the LoadBalancer service, 
allowing you to access it using an external IP.
A LoadBalancer service in Kubernetes is a way to expose your application to the outside world through 
a single external IP address that automatically distributes traffic to the underlying pods.

conclusion:
execute docker build to execute dockerfile run the commands without cmd command but docker start execute the just cmd command run app
development and service in yml file the development create the app but the service is prepare the app to be accessable 
minikube use it local Kubernetes
execute the command minikube start to run Kubernetes
StatefulSet to store data
kubernetes it simplifies the work from docker for example when i run the app from docker i need to activate the spring boot app i need 
to operate the workload contianer and postgress container to operate the app but with kubernetes i do'nt need to do it
the kubernetes do all the work operate the spring boot and postgress 
helm chart it simplifies the work from without it without helm chart and need to compile all the files and use it static data for example
i need to execute the two command below to run the app
kubectl apply -f k8s/petclinic.yml //deployment
kubectl apply -f k8s/db.yml
but with helm chart use it dynamic data can i change the data from values.yml it is very useful and run one command to create all the service and deployment
i execute the command below and it create all the configuration by one
helm install or upgrade petclinic-release ./petclinic-chart
use ingress to create url app
ingress steps:
enable ingress in minikube
minikube addons enable ingress
1-minikube start --addons=ingress
2-create petclininc-ingress.yaml
3-C:\Windows\System32\drivers\etc\hosts add 127.0.0.1 petclinic.local
install nginx 
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install nginx-ingress ingress-nginx/ingress-nginx --namespace kube-system
minikube tunnel // to run with ingress must be activate to run the app with kubernetes and ingres

minikube tunnel simulates that behavior by creating a route between your local machine and the LoadBalancer service, 
allowing you to access it using an external IP.

A LoadBalancer service in Kubernetes is a way to expose your application to the outside world through 
a single external IP address that automatically distributes traffic to the underlying pods.

Using NGINX as an Ingress Controller in Kubernetes gives you a central, flexible, and powerful way to manage access to multiple services in your cluster

A Kubernetes cluster is a set of machines (real or virtual) that work together to run containerized applications. 
It manages your applications' deployment, scaling, networking, and availability.

A Pod is the smallest and simplest unit in Kubernetes. It represents one or more containers that are:

Deployed together

Share the same network (IP/port space)

Can share storage volumes

A Node is a machine (physical or virtual) that runs your application containers in Kubernetes. It’s basically a worker in the cluster.
A NodePort service in Kubernetes:
Exposes your app on a static port on every Node’s IP, so you can access it from outside the cluster using NodeIP:NodePort.

run project:
requiremnets:windows os,docker desktop,minikube,helm
choco install kubernetes-helm
minikube start --addons=ingress
install nginx 
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install nginx-ingress ingress-nginx/ingress-nginx --namespace kube-system
minikube tunnel // to run with ingress must be activate to run the app with kubernetes and ingres
in C:\Windows\System32\drivers\etc\hosts add 127.0.0.1 petclinic.local
git clone from github
docker build -t dsyer/petclinic -f .devcontainer/Dockerfile . //in petclinic.yml spec container image dsyer/petclinic build dockerfile
docker compose up postgres and rename the container to postgress//run postgres service
helm install or upgrade petclinic-release ./petclinic-chart
minikube service petclinic