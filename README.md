# k8s-deployments strategies

- **Recreate**
- **Rolling Update**
- **Blue-Green Deployment**
- **Canary Release**

#### Prerequisites

- Docker setup: https://docs.docker.com/engine/install/
- Kubectl installation: https://kubernetes.io/docs/tasks/tools/
- Minikube setup : https://minikube.sigs.k8s.io/docs/start/

- Yaml script basics
- kubernetes basics 

```
docker version

kubectl version

minikube version

helm version

minikube start
```

#### Recreate deployment

Terminates all existing instances of the application and creates new replicas with the updated version

in deployment configuration

```
spec:
  replicas : 2
  strategy: 
    type: Recreate

```

```
kubectl apply -f Recreate/deployment.yml
kubectl apply -f Recreate/service.yml

kubectl get pods -w

kubectl delete -f Recreate/deployment.yml
kubectl delete -f Recreate/service.yml

```

#### Rolling update deployment

Gradually updates the application by replacing old replicas with new ones

```
spec:
  replicas : 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1

```

- `maxSurge` specifies the maximum number of replicas that can be created above the desired number of replicas during the update process. In this case, it allows only one additional replica to be created at a time.

- `maxUnavailable` specifies the maximum number of replicas that can be unavailable (due to termination or failure) during the update process. In this case, it allows only one replica to be unavailable at a time.

```
kubectl apply -f RollingUpdate/deployment.yml
kubectl apply -f RollingUpdate/service.yml

kubectl get pods -w

kubectl delete -f RollingUpdate/deployment.yml
kubectl delete -f RollingUpdate/service.yml

```



#### Blue Green Deployment

Blue-green deployment is a deployment strategy that involves running two identical environments, one called "blue" (the currently running version) and the other called "green" (the new version). The strategy involves directing all traffic to one of the environments while the other remains idle. 

```
kubectl apply -f Blue-Green/blue-deployment.yml
kubectl apply -f Blue-Green/green-deployment.yml

kubectl apply -f Blue-Green/service.yml


kubectl delete -f Blue-Green/blue-deployment.yml
kubectl delete -f Blue-Green/green-deployment.yml
kubectl delete -f Blue-Green/service.yml

```


#### Canary deployment

Canary deployment is a deployment strategy that introduces a new version of an application to a subset of users or traffic before making it available to the entire user base. This allows you to test the new version in a controlled environment and gather feedback before performing a full rollout. 

```
kubectl apply -f Canary/my-app-canary-deployment.yml
kubectl apply -f Canary/my-app-deployment.yml
kubectl apply -f Canary/service.yml

for i in `seq 1 10`; do curl http://192.168.49.2:31988/; sleep 1; done

kubectl delete -f Canary/my-app-deployment.yml
kubectl delete -f Canary/my-app-canary-deployment.yml
kubectl delete -f Canary/service.yml

```

