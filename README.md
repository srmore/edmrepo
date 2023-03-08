##START MINIKUBE
minikube start --cpus 3 --memory 3072 --driver=hyperv


##CREATE SECRET FOR REPO
kubectl create secret docker-registry edm-repo --docker-server=https://index.docker.io/v1/ --docker-username=username --docker-password=password --docker-email=useremail
kubectl get secret  edm-repo --output=yaml

##CREATE SECRET FOR EDM APP
kubectl apply -f ./edm-secret.yaml

##CREATE PERSISTENT VOLUME
kubectl apply -f ./storage-volume.yaml

##CREATE DB Deployment
kubectl apply -f ./postgres-db.yaml

##CREATE APP Deployment
kubectl apply -f ./kubernetes.yaml

##DELETE DEPLOYMENT
kubectl delete deployment db 
kubectl delete deployment edm
kubectl delete service db
kubectl delete service edm-balancer
kubectl delete pvc edm-pvc
kubectl delete pv edm-pv

##GET PODS
kubectl get pods
kubectl get service
kubectl get pvc

##GET SERVICES
kubectl get services


##DELETE CHART
helm delete edm-test -n edm-test

##INSTALL CHART
helm install edm-test ./edm-helm -n edm-test


##PUSH IMAGE FROM DOCKER HUB TO AWS ECR
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 322854463947.dkr.ecr.ap-south-1.amazonaws.com
docker tag sm-edm-repo:latest 322854463947.dkr.ecr.ap-south-1.amazonaws.com/sm-edm-repo:latest
docker push 322854463947.dkr.ecr.ap-south-1.amazonaws.com/sm-edm-repo:latest

## Now change the image name and tag name in values.yaml file like 322854463947.dkr.ecr.ap-south-1.amazonaws.com/sm-edm-repo:latest