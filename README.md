This project is a test to deploy and run the capella-collab-manager.

## Initialization
Some prerequisites commands have been executed to satisfy required configuration :  
* Docker >= 20.10.X
* kubectl >= 1.24 (Stargazer)
* helm >= 3.9.X
* Make >= 3.82, recommended 4.X
* Python >= 3.10
* k3d - a lightweight k8s cluster
All commands are detailed in file ["Prerequisites_installation.md"](/Prerequisites%20installation/Prerequisites%20installation.md)

## Attempt_2024-10-29 - v4.10.0
```bash
git clone --recurse-submodules https://github.com/DSD-DBS/capella-collab-manager.git
cd capella-collab-manager
make create-cluster reach-registry
export DOCKER_REGISTRY=ghcr.io/dsd-dbs/capella-collab-manager
export CAPELLACOLLAB_SESSIONS_REGISTRY=ghcr.io/dsd-dbs/capella-dockerimages
DEVELOPMENT_MODE=1 make helm-deploy open
```
  
This attempt has been done with capella-collab-manager v4.10.0.  
This attempt allows to run all pods except the `dev-backend` one.  
The "Capella Collaboration Manager" portal can be opened on the localhost (`https://localhost/`), but some elements are missing.  
More detailed logs are availabled in this file ["Logs_2024-10-29.md"](/Attempt_2024-10-29_1/Logs_2024-10-29.md).  

![](/Attempt_2024-10-29_1/local_host_missing_backend.png)

## Fix helm template
The Pod Events indicate that the Liveness and Readiness probes fail: Get "http://10.42.0.36:8000/healthcheck": dial tcp 10.42.0.36:8000: connect: connection refused. Remove the probes in the Helm template and redeploy.
https://github.com/DSD-DBS/capella-collab-manager/blob/main/helm/templates/backend/backend.deployment.yaml#L69 / https://github.com/DSD-DBS/capella-collab-manager/blob/main/helm/templates/backend/backend.deployment.yaml#L74

## Environment clean up
Theses commands allow to clean up the environment, and are executed after each attempt.  
```bash
make delete-cluster
k3d registry delete k3d-myregistry.localhost
```

Now the platform is running.  
More detailed here : [Notes](/Attempt_2024-10_31_1/Notes.md)  