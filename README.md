## Project Overview

This assignment deploys the provided TrustBank fraud detection API using Kubernetes, first using Minikube with GitHub Codespaces and then through Azure Container Apps. To run the Kubernetes deployment in Codespaces, execute `bash scripts/local_up.sh`. Deployment evidence is available in the `screenshots/` directory.

### Kubernetes Deployment

There are always a minimum of 3 replicas running. The Horizontal Pod Autoscalar (HPA) adjusts the number of pods to maintain a target average CPU utilization of 40%, scaling up to a maximum of eight replicas as needed. Liveness and readiness probes use the `/health` endpoint to monitor pod health and determine whether pods are ready to receive traffic. A LoadBalancer Service provides a stable endpoint for routing requests to the available pods.

### Zero-downtime updates
Two methods were demonstrated for zero-downtime updates. The first was a rolling update that transitioned replicas from v1 to v2 with `maxUnavailable: 0` configured to maintain the requried number of replicas during the update. The second method was blue-green deployment, where the current version was labeled as blue and the new verion was labeled as green. The blue and green versions are swapped, making the version change live. The Service selector was changed to route traffic from blue to green, demonstrating a live cutover, and then changed back to blue to demonstrate rollback.

### Azure Deployment
The fraud detection API was deployed to Azure Container Apps using West US 3. The `/health` endpoint returned a healthy status, and the provided smoke test confirmed that `/predict` returned HTTP 200. All Azure resources were torn down and deleted following completion of the assignment. 

### Respository
This repository was created from the instructor-provided GitHub template. The original `README-hw4.md` contains the detailed set up and demonstration instructions.

The following changes were made:
- `deployment.yaml` has 250m and 192Mi limits and the owner label was added
- `hpa.yaml` is set to 40% CPU and max 8 replicas
- a folder named `screenshots/` was added and 8 screenshots were uploaded
- `ANSWERS.md` was completed
- this `README.md` was created
