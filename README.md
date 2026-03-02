## **TP kubernetes-minikube par DJibril DAHOUB**
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

#### Lien de l'image publiée : 
https://hub.docker.com/repository/docker/djibrildh/myservice
