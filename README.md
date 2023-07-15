# k8s-deployments
Kubernetes deployment strategies


- Rolling Update: This strategy is the default deployment strategy in Kubernetes. It gradually replaces old instances with new ones by incrementally scaling up the new version and scaling down the old version.

- Blue-Green Deployment: In a Blue-Green deployment, you have two identical environments, one representing the existing production environment (Blue) and the other representing the new version (Green). Traffic is initially routed to the Blue environment. Once the Green environment is ready and tested, traffic is switched from Blue to Green, making it the new production environment.

- Canary Release: Canary deployment is a technique where a new version of an application is deployed to a subset of users or traffic. This allows you to test the new version in a production-like environment with limited impact. If the new version performs well, traffic can gradually be increased. If issues are detected, you can quickly roll back.

- A/B Testing: A/B testing involves deploying multiple versions of an application simultaneously and splitting traffic between them. It allows you to compare the performance and user experience of different versions in a controlled manner.

- Rolling Restart: This strategy involves restarting the application pods one at a time to apply configuration changes or updates. It is useful when you need to reload configuration files or apply changes that do not require a full deployment.

- Blue-Green-Canary: This strategy combines elements of Blue-Green deployment and Canary Release. It allows for more controlled testing by gradually shifting traffic from Blue to Green while also monitoring and validating the new version using a small percentage of traffic.


