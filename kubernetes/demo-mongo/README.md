## Demo: MongoExpress and MongoDB
2 pods (mongoexpress, mongodb), 2 service (internal service, external service), 1 configmap, and 1 secret.

## MongoDB Secret
- Create a secret YAML configuration `mongodb-secret.yaml`. 
- Under data you can include your key-value pairs.
- The key should be base64 encoded. Use `echo -n 'sample_value_of_key' | base64` to get base64 encoded values.
- Apply and create the secret `kubectl apply -f mongodb-secret.yaml`.
- Get secrets `kubectl get secrets`.

## MongoDB Deployment
- Review the `mongodb.yaml` file. Mongo runs on port 27017 `containerPort` and requires secrets `secretKeyRef`.
- Apply `kubectl apply -f mongodb.yaml` to create the deployment.
- First check the status of deployment `kubectl get deployments`.
- If deployment is not ready, check the status of pods `kubectl get pods`.
- If the pod shows an error, analyse it using `kubectl describe pod <pod-name>`.
- The pod might face issue while pulling the data internally. You can use `minikube ssh docker pull mongo` to pull image in minikube seperately.

## MongoDB Service
- Review the `mongodb.yaml` file. `---` is used as a document seperater for deployment and service.
- Apply `kubectl apply -f mongodb.yaml` to create the service.
- Get the service status `kubectl get services`.
- Fetch further details using `kubectl describe service mongodb-service`.

## MongoDB ConfigMap
- Review the `mongodb-configmap.yml` file. Database url here is same as what is referred by `mongodb-service` service.
- Apply `kubectl apply -f mongodb-configmap.yml` to create the configmap.
- Use `kubectl get configmaps` to fetch config map list.

## Mongo Express Deployment
- Review the `mongo-express.yaml` file. Mongo runs on port 27017 `containerPort` and requires secrets `secretKeyRef` and config maps `configMapKeyRef`.
- Execute `minikube ssh docker pull mongo-express` to pull image in minikube seperately.
- Apply `kubectl apply -f mongo-express.yaml` to create the deployment.
- First check the status of deployment `kubectl get deployments`.
- If deployment is not ready, check the status of pods `kubectl get pods`.
- If the pod shows an error, analyse it using `kubectl describe pod <pod-name>`.
- You can check the log of the pod using `kubectl logs <pod-name>`.

## Mongo Express Service (External)
- Review the `mongo-express.yaml` file. `---` is used as a document seperater for deployment and service.
- External service is denoted by `type: LoadBalancer` and `nodePort: 30000` is what will be exposed to the browser.
- Apply `kubectl apply -f mongo-express.yaml` to create the service.
- Get the service status `kubectl get services`.
- Fetch further details using `kubectl describe service mongo-express-service`.
- To open Mongo Express first get the CLUSTER-IP of `mongo-express-service` using `kubectl get services` and then execute `minikube service mongo-express-service`.
