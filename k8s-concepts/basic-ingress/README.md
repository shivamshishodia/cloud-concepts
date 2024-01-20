## Setup K8s Dashboard
- Execute `minikube ssh docker pull kubernetesui/dashboard:v2.7.0`.
- Apply K8s Dashboard `kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml`.
- Use `kubectl get all -n kubernetes-dashboard` to analysis K8s dashboard namespace.
- Execute `kubectl proxy` to start serving on [127.0.0.1:8001](127.0.0.1:8001).
- Navigate to [kubernetes-dashboard](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login).

## Ingress
- Install an ingress controller pod. We install one via `minikube addons enable ingress`.
- If the above command fails, execute the following commands.
```
minikube ssh docker image pull k8s.gcr.io/ingress-nginx/controller:v1.2.1
minikube ssh docker image pull k8s.gcr.io/ingress-nginx/kube-webhook-certgen:v1.1.1
minikube addons enable ingress --alsologtostderr
```
- Use `kubectl get all -n kubernetes-dashboard` to get service name and service port.
- Review `dashboard-ingress.yaml`. The namespace is `dashboard-ingress`, service name is `kubernetes-dashboard` and service port is `443`.
- Apply using `kubectl apply -f dashboard-ingress.yaml`
- Fetch the IP address using `kubectl get ingress -n kubernetes-dashboard`.
- You now have to create mapping in your `etc/hosts` file for `<IP> dashboard.com`.
- You will be able to browse K8s dashboard on `dashboard.com`.
