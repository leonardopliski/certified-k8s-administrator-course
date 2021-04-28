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

### Taints

Create a taint on a node:

kubectl taint nodes node-name key=value:taint-effect

Available taint effects:

- NoSchedule
- PreferNoSchedule
- NoExecute

Remove one taint

kubectl taint nodes master node-role.kubernetes.io/master:NoSchedule-

### Labels

Label a node with the 'size=Large'

kubectl label node kind-control-plane size=Large

Get labels of a node

kubectl get node kind-control-plane --show-labels

### Logging

Official k8s logging & monitoring solution (Metrics Server):

kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

Get nodes usage:

kubectl top node

Get internal pod logs:

kubectl logs -f event-simulator-pod

### ConfigMap

Create a configmap called `app-config`:

kubectl create configmap app-config --from-literal=APP_COLOR=blue -o yaml --dry-run=client > config-map.yaml

### Secrets

Create a secret called `app-secret`:

kubectl create secret generic app-secret --from-literal=DB_HOST=mysql --from-literal=DB_USER=root --from-literal=DB_PASSWORD=passwrd

### Utils

Get kube-system namespace pods

kubectl -n kube-system get pods

Explain the pod command 'tolerations' section:

kubectl explain pod --recursive | grep -A5 tolerations

### Cluster Maintenance

OS Upgrades:

#### Drain

Pods are gracefully terminated from the node that they are on and recreated on another:

kubectl drain node-1

#### Uncordon

Enable pod scheduling on node again:

kubectl uncordon node-1

#### Cordon

Mark the node as unschedulable:

kubectl cordon node-1

### Cluster Upgrade Process

Upgrade the kubeadm first:

apt-get upgrade -y kubeadm=1.12.0-00

kubeadm upgrade apply v1.12.0

Upgrade kubelet:

apt-get upgrade -y kubelet=1.12.0-00

systemctl restart kubelet

kubectl drain node-1

apt-get upgrade -y kubeadm=1.12.0-00
apt-get upgrade -y kubelet=1.12.0-00
kubeadm upgrade node config --kubelet-version v1.12.0

systemctl restart kubelet

kubectl uncordon node-1
