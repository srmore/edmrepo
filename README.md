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