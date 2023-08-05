### K8s Deployment sample application


**version 1**
```
docker build -t my-node-app:v1 .

docker run -d -p 3000:3000 my-node-app:v1


docker tag my-node-app:v1 veerasolaiyappan/my-node-app:v1
docker push veerasolaiyappan/my-node-app:v1
```


**version 2**
```
docker build -t my-node-app:v2 .

docker run -d -p 3000:3000 my-node-app:v2


docker tag my-node-app:v2 veerasolaiyappan/my-node-app:v2
docker push veerasolaiyappan/my-node-app:v2
```