# k8s-deployments strategies

- **Recreate**

- **Rolling Update**

- **Blue-Green Deployment**

- **Canary Release**


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

kubectl delete -f Recreate/deployment.yml
kubectl delete -f Recreate/service.yml

```

#### Rolling update deployment

```
kubectl apply -f RollingUpdate/deployment.yml
kubectl apply -f RollingUpdate/service.yml

kubectl set image deployment/my-app my-app=nginx:1.25.0

kubectl rollout status deployment/my-app


kubectl delete -f RollingUpdate/deployment.yml
kubectl delete -f RollingUpdate/service.yml

```


#### Canary deployment

Canary deployment is a deployment strategy that introduces a new version of an application to a subset of users or traffic before making it available to the entire user base. This allows you to test the new version in a controlled environment and gather feedback before performing a full rollout. Here's how you can implement canary deployment in Kubernetes:

```
kubectl apply -f Canary/my-app-deployment.yaml
kubectl apply -f Canary/service.yaml


kubectl apply -f Canary/my-app-canary-deployment.yaml



kubectl delete -f Canary/my-app-deployment.yaml
kubectl delete -f Canary/my-app-canary-deployment.yaml
kubectl delete -f Canary/service.yaml

```

#### Blue Green Deployment

Blue-green deployment is a deployment strategy that involves running two identical environments, one called "blue" (the currently running version) and the other called "green" (the new version). The strategy involves directing all traffic to one of the environments while the other remains idle. Here's how you can implement blue-green deployment in Kubernetes:

```
kubectl apply -f Blue-Green/blue-deployment.yaml
kubectl apply -f Blue-Green/green-deployment.yaml

# Scale up the blue Deployment (optional if you already set replicas in the Deployment YAML)
kubectl scale deployment my-app-blue --replicas=3

# Scale up the green Deployment
kubectl scale deployment my-app-green --replicas=3

# Scale down the blue Deployment
kubectl scale deployment my-app-blue --replicas=0


kubectl apply -f my-app-green-service.yaml



```

