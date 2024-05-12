## Hosting MediaWiki on Minikube Cluster using Helm 

### Introduction 

This documentation provides detailed steps for hosting MediaWiki on a Minikube cluster using Helm. MediaWiki is a free and open-source wiki application, widely used for creating and managing wikis. 

  
### Prerequisites 

1. Minikube installed and running. 

2. Helm installed on Minikube. 

3. Docker installed locally. 

4. Dockerfiles for MediaWiki and MySQL created and pushed to DockerHub. 

5. Basic understanding of Kubernetes concepts like Pods, Deployments, Services, Ingress, etc. 

  

### Step 1: Set up Dockerfiles 

Create Dockerfiles for MediaWiki and MySQL. Ensure they are properly configured and pushed to DockerHub. 

  

### Step 2: Create Helm Chart 

Create a Helm chart named `mediawiki-helm-chart` with the following structure: 

``` 

mediawiki-helm-chart/ 

  │ 

  ├── charts/ 

  ├── templates/ 

  │   ├── hpa.yaml 

  │   ├── mediawiki-deployment.yaml 

  │   ├── mediawiki-ingress.yaml 

  │   ├── mediawiki-service.yaml 

  │   ├── mysql-deployment.yaml 

  │   └── mysql-service.yaml 

  │ 

  ├── values.yaml 

  └── Chart.yaml 

``` 

  

### Step 3: Configure Helm Chart 

1. Update `values.yaml` with necessary configuration values such as image names, environment variables, etc. 

2. Define resource configurations in `mediawiki-deployment.yaml` and `mysql-deployment.yaml`. 

3. Define service configurations in `mediawiki-service.yaml` and `mysql-service.yaml`. 

4. Configure Ingress in `mediawiki-ingress.yaml` to expose MediaWiki to external traffic. 

  

### Step 4: Deploy Helm Chart 

Run the following commands to deploy the Helm chart: 

```bash 

helm install mediawiki mediawiki-helm-chart 

``` 

  

### Step 5: Expose MediaWiki Screenshot from 2024-05-13 04-05-00

1. Run `minikube tunnel` to expose MediaWiki service. 

2. Map the Minikube Ingress IP with a custom DNS name (e.g., `wikimedia.local`) in `/etc/hosts`. 

  ![image](https://github.com/Rahulrajtiwari/mediawiki/assets/27560388/6a3e8631-ca61-46fa-b034-37038cf748d5)


### Step 6: Access MediaWiki 

Access MediaWiki via the configured DNS name (e.g., `wikimedia.local`) in your web browser. 

![image](https://github.com/Rahulrajtiwari/mediawiki/assets/27560388/57d87469-6d00-432f-a510-f5bde18467e2)
 

### Optimization Scope 

- **Karpenter Integration**: Utilize Karpenter with Horizontal Pod Autoscaler (HPA) for better scaling in a cost-optimized way, ensuring resources are provisioned only when required. 

- **AWS Secret Manager Integration**: Implement AWS Secret Manager for securely storing database credentials, enhancing security and compliance. 

- **CI/CD Pipeline Creation**: Establish a CI/CD pipeline for automated deployment of MediaWiki updates, improving development velocity and release reliability. 

- **Docker Optimization**: Optimize Dockerfile instructions to minimize the number of layers created in the image. 

- Combine multiple commands into a single `RUN` instruction to reduce the number of layers and improve build speed. 

- **Additional Optimization**: Explore other optimization strategies such as implementing caching mechanisms, optimizing container resource limits, and leveraging Kubernetes scheduling policies for better resource utilization. 

  

### Conclusion 

By following these steps and incorporating optimization strategies, you have successfully hosted MediaWiki on a Minikube cluster using Helm. You can now enjoy the benefits of MediaWiki for creating and managing wikis while ensuring efficient resource utilization and enhanced security. 
