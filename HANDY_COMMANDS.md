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
