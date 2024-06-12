# Coworking Space Service Extension
The Coworking Space Service is a set of APIs that enables users to request one-time tokens and administrators to authorize access to a coworking space. This service follows a microservice pattern and the APIs are split into distinct services that can be deployed and managed independently of one another.

For this project, you are a DevOps engineer who will be collaborating with a team that is building an API for business analysts. The API provides business analysts basic analytics data on user activity in the service. The application they provide you functions as expected locally and you are expected to help build a pipeline to deploy it in Kubernetes.

## Getting Started

### Dependencies
#### Local Environment
1. Python Environment - run Python 3.6+ applications and install Python dependencies via `pip`
2. Docker CLI - build and run Docker images locally
3. `kubectl` - run commands against a Kubernetes cluster
4. `helm` - apply Helm Charts to a Kubernetes cluster

#### Remote Resources
1. AWS CodeBuild - build Docker images remotely
2. AWS ECR - host Docker images
3. Kubernetes Environment with AWS EKS - run applications in k8s
4. AWS CloudWatch - monitor activity and logs in EKS
5. GitHub - pull and clone code

### Setup
#### 1. Configure a Database
Set up a Postgres database using a Helm Chart.

1. Configure AWS Account: Run the aws configure command to set up your AWS account credentials.
2. Create Amazon ECR Repository: Set up an ECR repository to store your Docker images.
3. Set Up Amazon CodeBuild: Create a CodeBuild project linked to your GitHub repository to automate your builds.
4. Create buildspec.yaml: Define a buildspec.yaml file to specify how to build and push Docker images to ECR.
5. Push Changes to GitHub: Commit and push your changes to your GitHub repository.
6. Trigger CodeBuild: CodeBuild will automatically start the build process and push the Docker image to ECR upon detecting changes.
7. Apply Configurations: Use kubectl apply -f configmap.yaml to apply configuration properties and secrets.
8. Deploy Application: Deploy your application using kubectl apply -f coworking.yaml.


* `DB_USERNAME`
* `DB_PASSWORD`
* `DB_HOST` (defaults to `127.0.0.1`)
* `DB_PORT` (defaults to `5432`)
* `DB_NAME` (defaults to `postgres`)

The benefit here is that it's explicitly set. However, note that the `DB_PASSWORD` value is now recorded in the session's history in plaintext. There are several ways to work around this including setting environment variables in a file and sourcing them in a terminal session.

## Project Instructions
1. Set up a Postgres database with a Helm Chart
2. Create a `Dockerfile` for the Python application. Use a base image that is Python-based.
3. Write a simple build pipeline with AWS CodeBuild to build and push a Docker image into AWS ECR
4. Create a service and deployment using Kubernetes configuration files to deploy the application
5. Check AWS CloudWatch for application logs

### Deliverables
1. `Dockerfile`
2. Screenshot of AWS CodeBuild pipeline
3. Screenshot of AWS ECR repository for the application's repository
4. Screenshot of `kubectl get svc`
5. Screenshot of `kubectl get pods`
6. Screenshot of `kubectl describe svc <DATABASE_SERVICE_NAME>`
7. Screenshot of `kubectl describe deployment <SERVICE_NAME>`
8. All Kubernetes config files used for deployment (ie YAML files)
9. Screenshot of AWS CloudWatch logs for the application
10. `README.md` file in your solution that serves as documentation for your user to detail how your deployment process works and how the user can deploy changes. The details should not simply rehash what you have done on a step by step basis. Instead, it should help an experienced software developer understand the technologies and tools in the build and deploy process as well as provide them insight into how they would release new builds.


### Stand Out Suggestions
1. Reasonable Memory and CPU Allocation
   Specify memory and CPU limits in your Kubernetes deployment to ensure efficient resource use. For example, set resources.requests to memory: "256Mi" and cpu: "500m", and resources.limits to memory: "512Mi" and cpu: "1000m". This prevents resource overuse and maintains cluster stability.

2. Best AWS Instance Type for the Application
   Use an AWS EC2 t3.medium instance, which offers a balance of 2 vCPUs and 4 GiB of memory, suitable for moderate workloads. It provides burstable performance and is cost-effective for variable workloads.

3. Cost-Saving Strategies
   Implement auto-scaling to adjust resources based on demand. Use AWS Spot Instances for non-critical tasks to reduce costs. Regularly review and right-size instances to avoid over-provisioning. Consider AWS Savings Plans or Reserved Instances for long-term workloads to get significant discounts.
