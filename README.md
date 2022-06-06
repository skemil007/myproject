# Node.js Hello World

This Assessment contains a minimal hello world application written in Node. This repo will document the many ways you can deploy this application.

## Run locally

```bash
npm install
npm start
```

## Run in a container

```bash
docker build -t node-hello-world:latest .
docker run -it -p 8080:8080 --name node-hello-world node-hello-world:latest
```

## Run on Kubernetes

Ensure the container image URL is updated in [deployment.yaml](config/deployment.yaml).

**Note:** Add imagepullsecrets in k8s yaml if using private registry.

```bash
# Build and push to Docker Registry
# Update the container registry to match your own namespace
docker build -t registrypath/node-hello-world:latest .
docker push registrypath/node-hello-world:latest

# Deploy to K8S
kubectl config current-context
kubectl apply -f config/
kubectl rollout status deployment/node-hello-world
kubectl get services -o wide
```
## Build and Deploy with GitHub Actions

Ensure the below credentails are added into githib secrets.


- DOCKERHUB_USERNAME
- DOCKERHUB_TOKEN
- DOCKERHUB_USERNAME
- GCP_PROJECT
- GCP_CREDENTIALS

Update the GCP cluster name and region in the github workflow file.