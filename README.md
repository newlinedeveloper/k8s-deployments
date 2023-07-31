# k8s-deployments
Kubernetes deployment strategies

- **Recreate**

- **Rolling Update**

- **Blue-Green Deployment**

- **Canary Release**:


#### Recreate deployment

```
kubectl apply -f Recreate/deployment.yml
kubectl apply -f Recreate/service.yml

kubectl delete -f Recreate/deployment.yml
kubectl delete -f Recreate/service.yml

```

#### Recreate deployment

```
kubectl apply -f Recreate/recreate.yml

kubectl delete -f Recreate/recreate.yml

```


