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
 


### Troubleshooting and Optimization:

1. **Scaling Issues Identification:**
   - Monitor the application performance metrics such as CPU usage, memory consumption, and response times to identify any scaling issues.
   - **Karpenter Integration**: Utilize Karpenter with Horizontal Pod Autoscaler (HPA) for better scaling in a cost-optimized way, ensuring resources are provisioned only when required. 

2. **Suggestions for Resolving Scaling Issues:**
   - **Optimize Docker Images:**
     - Review Dockerfiles for both MediaWiki and MySQL to ensure efficient image building.
     - Minimize the number of layers in Dockerfiles to reduce image size and build time.
     - Utilize multi-stage builds to separate build dependencies from runtime dependencies, resulting in smaller final images.
   
   - **Resource Requests and Limits:**
     - Set appropriate resource requests and limits for MediaWiki and MySQL containers to ensure optimal resource utilization.
     - Adjust resource requests and limits based on workload characteristics and observed performance metrics.

   - **Database Optimization:**
     - Fine-tune MySQL configuration parameters such as buffer sizes, connection limits, and query cache settings for optimal performance.
     - Monitor database performance metrics using tools like MySQL Workbench or Prometheus to identify and address any database bottlenecks.

   - **Caching Strategies:**
     - Implement caching mechanisms such as Redis or Memcached to reduce database load and improve application responsiveness.
     - Configure MediaWiki to utilize caching features for frequently accessed content to reduce database queries.

   - **Content Delivery Network (CDN):**
     - Integrate a CDN such as Amazon CloudFront or Cloudflare to cache static assets and accelerate content delivery to end-users.
     - Configure caching policies to minimize latency and improve overall application performance.

   - **Database Scaling Options:**
     - Consider using managed database services such as Amazon RDS or Google Cloud SQL for MySQL to offload database management tasks and facilitate horizontal scaling.
     - Evaluate sharding or partitioning strategies to horizontally partition data across multiple database instances for improved scalability.

- **AWS Secret Manager Integration**: Implement AWS Secret Manager for securely storing database credentials, enhancing security and compliance. 

- **CI/CD Pipeline Creation**: Establish a CI/CD pipeline for automated deployment of MediaWiki updates, improving development velocity and release reliability. 
  

### Conclusion 

By following these steps and incorporating optimization strategies, you have successfully hosted MediaWiki on a Minikube cluster using Helm. You can now enjoy the benefits of MediaWiki for creating and managing wikis while ensuring efficient resource utilization and enhanced security. 
