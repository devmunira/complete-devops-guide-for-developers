# MERN Application Deployment on Kubernetes

This project demonstrates deploying a MERN (MongoDB, Express.js, React.js, Node.js) application on Kubernetes with advanced features including:

- **Vertical Scaling**: Resource allocation and scaling
- **Auto-Healing**: Self-healing capabilities
- **Load Balancing**: Traffic distribution across pods
- **Blue-Green Deployment**: Zero-downtime deployments
- **Canary Deployment**: Gradual rollout strategy

## Architecture Overview

The application consists of two main services:

- **MongoDB**: Document database (mongo:5.0)
- **Mongo-Express**: Web-based MongoDB admin interface (mongo-express:latest)

## Quick Deployment

### 1. Create Kubernetes Resources

```bash
# Create secrets for MongoDB credentials
kubectl apply -f secret.yml

# Deploy MongoDB with persistent storage
kubectl apply -f mongo-app.yml

# Create MongoDB service (ClusterIP)
kubectl apply -f mongo-service.yml

# Create ConfigMap for MongoDB connection
kubectl apply -f mongo-config.yml

# Deploy mongo-express application
kubectl apply -f express-webapp.yml

# Expose mongo-express service (NodePort: 30111)
kubectl apply -f webapp-service.yml
```

### 2. Verify Deployment

```bash
# Check pod status
kubectl get pods

# Check services
kubectl get svc

# Check deployments
kubectl get deployments
```

### 3. Access Application

- **Local/Minikube**: Access via minikube IP on port 30111
- **EC2/Cloud**: Use socat for external access:
  ```bash
  yum install socat -y
  socat TCP4-LISTEN:8080,fork,su=nobody TCP4:192.168.49.2:30111
  ```

## Advanced Features

### Vertical Scaling

The deployments are configured with resource requests and limits:

```yaml
resources:
  requests:
    memory: "64Mi"
    cpu: "250m"
  limits:
    memory: "128Mi"
    cpu: "500m"
```

### Auto-Healing

- **Health Checks**: Liveness and readiness probes
- **ReplicaSets**: Automatic pod replacement
- **Node Failure Recovery**: Pod rescheduling

### Load Balancing

- **Service Load Balancing**: Automatic traffic distribution
- **Session Affinity**: Sticky sessions when needed
- **Health-based Routing**: Traffic only to healthy pods

### Blue-Green Deployment

```bash
# Deploy new version (green)
kubectl apply -f mongo-express-v2.yml

# Switch traffic
kubectl patch svc webapp-service -p '{"spec":{"selector":{"version":"v2"}}}'

# Rollback if needed
kubectl patch svc webapp-service -p '{"spec":{"selector":{"version":"v1"}}}'
```

### Canary Deployment

```bash
# Deploy canary version (10% traffic)
kubectl apply -f mongo-express-canary.yml

# Gradually increase traffic
kubectl scale deployment mongo-express-canary --replicas=2

# Full rollout
kubectl scale deployment mongo-express --replicas=0
kubectl scale deployment mongo-express-canary --replicas=5
```

## Configuration Files

### MongoDB Deployment (`mongo-app.yml`)

- Persistent volume for data storage
- Resource limits and requests
- Health checks
- Secret-based authentication

### Mongo-Express Deployment (`express-webapp.yml`)

- Horizontal pod autoscaler
- Rolling update strategy
- ConfigMap for configuration
- Secret for database credentials

### Services

- **MongoDB Service**: ClusterIP for internal communication
- **Mongo-Express Service**: NodePort for external access

### Secrets & ConfigMaps

- **MongoDB Credentials**: Base64 encoded username/password
- **Database URL**: Service discovery configuration

## Monitoring & Troubleshooting

```bash
# View pod logs
kubectl logs <pod-name>

# Describe resources
kubectl describe pod <pod-name>
kubectl describe svc <service-name>

# Port forward for debugging
kubectl port-forward <pod-name> 8080:8081

# Check resource usage
kubectl top pods
kubectl top nodes
```

## Cleanup

```bash
# Delete all resources
kubectl delete -f .
# or
kubectl delete deployment,svc,secret,configmap -l app=mongo
kubectl delete deployment,svc -l app=webapp
```

## References

- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [MongoDB](https://www.mongodb.com/)
- [Mongo-Express](https://www.npmjs.com/package/mongo-express)
- [Kubernetes Deployment Strategies](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#deployment-strategies)
