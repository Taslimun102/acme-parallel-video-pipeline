# acme-parallel-video-pipeline


Setup Guide

1. Start the Local Kubernetes Cluster

This PoC is executed on a local Kubernetes cluster using Docker Desktop.
-->Open Docker Desktop.
-->Go to Settings → Kubernetes.
-->Enable Kubernetes and apply the changes.
-->Wait until Kubernetes is running.
   
Verify the cluster: "kubectl get nodes"



2. Install the Orchestration Tool (Argo Workflows)

Create the Argo namespace and install Argo Workflows: "kubectl create namespace argo", 
"kubectl apply -n argo -f https://raw.githubusercontent.com/argoproj/argo-workflows/stable/manifests/install.yaml"

Confirm installation: "kubectl get pods -n argo"


3. Build the Docker Image

Build the Docker image containing the provided Python scripts: "docker build -t acme/video-pipeline:dev -f docker/Dockerfile"



4. Create Persistent Storage

Create the Persistent Volume Claim used to share data between workflow phases: "kubectl apply -n argo -f argo/pvc.yaml"



5. Trigger the Workflow

Start the workflow execution: "kubectl create -n argo -f argo/workflow.yaml"



6. Monitor Execution

Check workflow and pod status: "kubectl get workflows -n argo" , "kubectl get pods -n argo"

To access the Argo UI: "kubectl -n argo port-forward deployment/argo-server 2746:2746" 
Open a browser and navigate to: "https://localhost:2746"
