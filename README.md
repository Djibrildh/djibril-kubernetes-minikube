## **TP kubernetes-minikube par Djibril DAHOUB**
L'objet de ce TP est d'explorer dans un premiers temps l'installation des technologies **Dockers** et **kubernetes-minikube**. 

#### Démarrage et vérification de Minikube
`minikube start`
`minikube profile list`

#### Récupération de l'image et du code
`git clone https://github.com/charroux/kubernetes-minikube`

#### Création et test de l'image Docker en local
`docker build -t myservice .`
`docker images`
`docker run -p 4000:8080 -t myservice`
`docker ps`
`docker stop [containerID]`

#### Publication de l'image sur le Docker Hub
`docker tag bfe60bfcbbb6 djibrildh/myservice:latest`
`docker login http://hub.docker.com`
`docker login`
`docker push djibrildh/myservice:latest`

#### Déploiement de l'application sur Kubernetes
`kubectl get nodes`
`kubectl create deployment myservice --image=efrei/myservice:1`
`kubectl get pods`
`kubectl describe pods`

#### Commandes à l'intérieur du Pod Kubernetes
`kubectl exec -it myservice-746766f779-sxvxp -- /bin/bash`
`ls`
`exit`

#### Gestion et mise à jour du Déploiement (Scale & Rollout)
`kubectl scale --replicas=2 deployment/myservice`
`docker tag myservice:latest djibrildh/my-image:v2`
`docker push djibrildh/my-image:v2`
`kubectl set image deployments/myservice myservice=djibrildh/my-image:v2`
`kubectl rollout status deployments/myservice`
`kubectl rollout undo deployments/myservice`

#### Exposition de l'application (Services)
`kubectl expose deployment myservice --type=NodePort --port=8080`
`minikube service myservice --url`
`kubectl delete service myservice`
`kubectl expose deployment myservice --type=LoadBalancer --port=8080`

#### Déploiement via fichiers de configuration (YAML)
`kubectl apply -f myservice-deployment.yml`
`kubectl apply -f myservice-service.yml`

#### Configuration de l'Ingress et routage
`minikube addons enable ingress`
`kubectl get pods -n ingress-nginx`
`kubectl apply -f ingress.yml`
`kubectl get ingress`
`sudo nano /etc/hosts` *(Ajout de 127.0.0.1 myservice.info en fin de document)*
`minikube tunnel`

#### Ajout d'un deuxième service (V2)
`kubectl apply -f myserviceV2-deployment.yml`
`kubectl apply -f myserviceV2-service.yml`

#### Lien de l'image publiée : 
https://hub.docker.com/repository/docker/djibrildh/myservice
