## Basic Kubectl Commands
- CRUD commands
```
Create deployment `kubectl create deployment [name]`
Edit deployment `kubectl edit deployment [name]`
Delete deployment `kubectl delete deployment [name]`
```
- Status of components `kubectl get (nodes|pod|services|replicaset|deployment)`.
- Debugging tools
```
Log to console `kubectl logs [pod name]`
Get Interactive tunnel `kubectl exec -it [pod name] -- bin/bash`
```

## Kubectl Practice
- Create deployment named as 'nginx-depl' `kubectl create deployment nginx-depl --image=nginx`.
- Get the deployments `kubectl get deployments`.
- Get the pods and wait for the pod to start `kubectl get pods`.
- Between deployment and pod there is another layer called replicaset `kubectl get replicasets`. You don't have to work on replicasets.
- Abstraction Layer: `deployment > replicaset > pod > container`. Everything below deployment is managed by K8s.
- Naming conventions: Deployment will be named as nginx-depl. Replicaset will named with added suffix as nginx-depl-c88549479. Pod will be having another suffix on top of replicaset and is named as nginx-depl-c88549479-hk4z2.
- Edit deployment. You will get back auto-generated config file `kubectl edit deployment nginx-depl`. After editing the file, old pods are terminated and new spawned.
- Log check inside pod `kubectl logs nginx-depl-5b59dcd777-ng6kn`.
- Interactive shell inside pod `kubectl exec -it nginx-depl-5b59dcd777-ng6kn -- bin/bash`.
- Delete a deployment `kubectl delete deployment nginx-depl`. This will delete everything underneath deployment (replicasets, pods, etc.).
- Apply usage to pick all the details from YAML config files `kubectl apply -f [config.yaml]`.
