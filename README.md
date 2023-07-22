# kubernetes-objects-yaml-config-guide

## Practice Guide:

`NB!`

Please ensure that you have both [docker desktop](https://www.docker.com/products/docker-desktop/), and [minikube](https://minikube.sigs.k8s.io/docs/start/) installed in your machine.

This is a basic Kubernetes practice guide that takes one through configuration, and integration of kubernetes namespaces, configmaps, services, deployments and pods.

### Setting up the required resources

* Create a namespace resource with the specified config in the `doctors-directory-namespace.yaml` file.

```
kubectl apply -f doctors-directory-namespace.yaml
```

* Create a deployment, service and pod resource to spin-up a mongodb instance with the specified config(s) in the `mongodb-deployment.yaml` file

```
kubectl apply -f mongodb-deployment.yaml
```

* Create a configMap resource to store the servers non-confidential data (environment variables). 

```
kubectl apply -f doctors-directory-server-configmap.yaml
```

* Create a configMap resource to store the clients non-confidential data (environment variables). 

```
kubectl apply -f doctors-directory-client-configmap.yaml
```

* Create a deployment, service and pod resource to spin-up a nodejs server instance with the specified config(s) in the `doctors-directory-server-deployment.yaml` file.

```
kubectl apply -f doctors-directory-server-deployment.yaml
```

* Create a deployment, service and pod resource to spin-up a react client instance with the specified config(s) in the `doctors-directory-client-deployment.yaml` file.

```
kubectl apply -f doctors-directory-client-deployment.yaml
```

* Define a context for the kubectl client to work in the `doctors-directory` namespace.

```
kubectl config set-context doctors-dir --namespace=doctors-directory --cluster=minikube --user=minikube
```

* Switch to the doctors-dir namespace.

```
kubectl config use-context doctors-dir
```

* Forward the ports running on your client and server apps in the cluster to your localhost

```
kubectl port-forward deployment/doctors-directory-server-deployment 5002:5002
```

```
kubectl port-forward deployment/doctors-directory-client-deployment 3000:3000
```


