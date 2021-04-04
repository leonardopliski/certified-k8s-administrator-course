### Create an NGINX Pod:

kubectl run nginx --image=nginx

### Generate a POD Manifest YAML and don't create it (dry run)

kubectl run nginx --image=nginx --dry-run=client -o=yaml

### Create a deployment:

kubectl create deployment --image=nginx nginx

### Generate a deployment YAML and don't create it (dry run)

kubectl create deployment --image=nginx nginx --dry-run=client -o=yaml

### Generate a deployment YAML file with 4 replicas and don't create it (dry run)

kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o=yaml > deployment-definition.yaml

### Scale a deployment

kubectl scale deployment nginx --replicas=4

### Apply specs in a declarative way:

kubectl apply -f nginx.yaml

### Services

Create a ClusterIP service to expose redis pod on port 6379

kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml

or

kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml

Create a service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes:

kubectl expose pod nginx --port=80 --name=nginx-service --type=NodePort --dry-run=client -o yaml
