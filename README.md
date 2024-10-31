# Kubernetes Mid-Term Submission

## Architecture and Components

The Kubernetes environment is composed of three primary services, each deployed using a `Deployment` and exposed with a `NodePort` `Service`:

1. **Linux Development Environment (Alpine)**
    - Simple Linux container with Alpine, replicating a basic development or testing environment.
    - **Replica count**: 3
    - **Port**: 80, exposed via `NodePort` on `30080`

2. **Database Service (Postgres)**
    - Provides database capabilities using PostgreSQL, configured for three replicas to ensure high availability.
    - **Environment Variables** for database configuration:
        - `POSTGRES_USER`: `admin`
        - `POSTGRES_PASSWORD`: `supersecretpassword`
        - `POSTGRES_DB`: `mydatabase`
    - **Port**: 5432, exposed via `NodePort` on `30081`

3. **Web Service Application (Hello Service)**
    - A sample "Hello World" application for demonstrating basic web service deployment and resource management.
    - **Replica count**: 3
    - **Port**: 8080, exposed via `NodePort` on `30082`

## Key Kubernetes Capabilities Implemented

This project incorporates several essential Kubernetes features to meet enterprise standards and project requirements:

1. **High Availability and Self-Healing**:
    - Each service is configured with three replicas managed by `ReplicaSets`, ensuring availability even during pod failures.
    - Kubernetes automatically recreates pods as needed to maintain the desired replica count, demonstrating self-healing.

2. **Scalability**:
    - The environment is designed for horizontal scaling. By adjusting the `replicas` count in the deployment manifests, the infrastructure can dynamically meet varying workload demands.

3. **Resource Management**:
    - Resource `requests` and `limits` are set for CPU and memory across all services, optimizing the allocation and distribution of computational resources.

4. **Networking and Service Communication**:
    - `NodePort` Services expose each application on specific ports, facilitating external access and service communication across the cluster.

5. **Declarative Configuration with Manifest Files**:
    - YAML manifests are used for all resource definitions, ensuring a declarative and version-controlled setup.

## Files Included

### Services

- `alpine-service.yaml`: Exposes the Alpine deployment on port `30080`.
- `postgres-service.yaml`: Exposes the Postgres deployment on port `30081`.
- `hello-service.yaml`: Exposes the Hello Service deployment on port `30082`.

### Deployments

- `alpine-deployment.yaml`: Defines the Alpine deployment with three replicas and specified resource limits.
- `postgres-deployment.yaml`: Defines the Postgres deployment with three replicas, environment variables, and specified resource limits.
- `hello-deployment.yaml`: Defines the Hello Service deployment with three replicas and specified resource limits.

## Requirements Addressed

This project meets the following specified requirements:

- **Pods and Deployments**: Each service is deployed as a pod managed by a deployment.
- **ReplicaSets**: Configured to maintain three replicas per service, enhancing availability.
- **Services and Networking**: NodePort services provide network exposure, while internal communication is set up via `ClusterIP`.
- **Resource Quotas and Management**: CPU and memory limits are set for each container, ensuring optimized resource utilization.
- **Environment Variables**: Used to configure the Postgres database credentials.
- **Declarative Management**: All configurations are maintained in YAML manifests for reproducibility and version control.



## Running the Project

1. **Deploy the Services**: Apply the YAML files to your Kubernetes cluster.
   ```bash
   kubectl apply -f ./deployment/deployment.yaml
   kubectl apply -f ./services/services.yaml

