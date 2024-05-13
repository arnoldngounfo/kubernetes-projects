TP 2 DEPLOYEZ VOTRE PREMIERE APPLICATION (minikube et eazylabs) :
Créez un repertoire Kubernetes-training et un sous-dossier tp-2 et copiez vos manifests à l’interieur mkdir -p Kubernetes-training/tp-2 cd Kubernetes-training/tp-2

Ecrivez un manifest pod.yml pour déployer un pod avec l’image mmumshad/simple-webapp-color en précisant que la color souhaitée est la rouge => Le manifeste vous est le suivant: text

lancez votre pod

kubectl apply -f pod.yml
vérifiez qu’il est bien en cours d’exécution

kubectl get po
kubectl describe po simple-webapp-color
exposez votre pod en utilisant la commande

kubectl port-forward <nom de votre pod> 8080:8080 –-address 0.0.0.0
kubectl port-forward simple-webapp-color 8090:8080 --address 0.0.0.0
vérifiez que l’application est bien joignagle en ouvrant votre VM sur le port 8080 supprimez votre pod

kubectl delete -f pod.yml
vérifiez que l’application est bien supprimer en actualisant votre VM sur le port 8080 ou en tappant la cmde

kubectl get po
Nous avons creer un objet de type pod, cependant nous allons passer à la creation d'un objet de type deploiement 2 replicas d’un pod nginx

creer le fichier nginx-deployment.yml Mettre le contenu suivant

notre script mis en place, lacons notre objet deployment

kubectl apply -f nginx-deployment.yml
verifions le nombre de nos objets de type deployment

kubectl get deploy
verifions le nombre de nos objets de type replicaset

kubectl get replicaset
verifions le nombre de nos objets de type pop

kubectl get po
passons a la version latest de nginx pour cela on va mettre a jour la version de nginx dans le container ensuite tapons

kubectl apply -f nginx-deployment.yml
on peut constater que le deployment reconfigure notre ressource

pour suivre l'evolution de la mise a jour de notre version on tape

kubectl get replicaset -o wide
pour visualiser l'évolution de notre cluster

watch kubectl get all
pour visualiser l'historique de notre deploiement

kubectl rollout history deployment/nginx-deployment
pour faire un rollback

kubectl rollout undo deployment/nginx-deployment
supprimez votre deployment

kubectl delete -f nginx-deployment.yml
Nous avons terminé avec l'approche déclarative, nous allons continué avec l'approche impérative pour pouvoir créé nos ressources

Supprimez toutes les ressources créées et recréez les en utilisant les commandes impératives

lancement du pod :    
# lancement du pod : 
kubectl run --image=mmumshad/simple-webapp-color --env="APP_COLOR=red" simple-webapp-color
# Suppression du pod :  
kubectl delete pod simple-webapp-color
# Lancement du deploy:  
kubectl create deployment --image=nginx:1.18.0 nginx-deployment
# Scaling du replicas:  
kubectl scale --replicas=2 deployment/nginx-deployment
# upgrade de version :  
kubectl set image deployment/nginx-deployment nginx=nginx
# pour suivre l'evolution de la mise a jour de notre version on tape 
kubectl get replicaset -o wide 
# Suppression du deploy :  
kubectl delete deployment/nginx-deployment
Enfin, poussez ce de tp sur votre github afin de conservez tous vos fichiers

cd ..
git init
git add . 
git commit -m "message de commit personnalisé"
git remote add origin http://url_repos_git
git push origin main
