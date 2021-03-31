### Namespaces

Internal k8s resources: kube-system

Resources that should be available for all users: kube-public

Default namespace: default

#### How to connect to some service within another namespace?

Syntax: \<svc-name\>.\<namespace\>.\<resource-type\>.\<domain>

mysql.connect("db-service.dev.svc.cluster.local")

#### Commands

Get 'kube-system' namespace pods:

kubectl get pods --namespace=kube-system

Create a namespace YAML definition file called 'dev':

kubectl create namespace dev --dry-run=client -o=yaml > dev-namespace-definition.yaml

Create a pod in the 'dev' namespace:

kubectl create -f pod-definition.yaml --namespace=dev

Switch to the 'dev' namespace:

kubectl config set-context $(kubectl config current-context) --namespace=dev

Get all pods of all namespaces:

kubectl get pods --all-namespaces
