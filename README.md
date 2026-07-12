## Cloud-Native Web Application on GKE - GitOps CI/CD & Disaster Recovery

# Cloud-Native Web Application on GKE — GitOps CI/CD & Disaster Recovery Platform

---

# Executive Summary

Modern organizations require reliable, automated, and scalable platforms to deliver applications quickly while maintaining security, availability, and operational stability.

This project demonstrates the design and implementation of a production-style cloud-native application delivery platform on **Google Kubernetes Engine (GKE)** using **Infrastructure as Code (Terraform), Containerization (Docker), Continuous Integration (GitHub Actions), GitOps Deployment (Argo CD), and Disaster Recovery (Velero).**

The platform automates the complete application lifecycle:

- Infrastructure provisioning
- Container image creation
- Continuous integration
- Kubernetes deployment
- GitOps-based application synchronization
- Backup and disaster recovery validation

The project simulates real-world operational challenges such as:

- Infrastructure failures
- Application deployment errors
- Configuration drift
- Accidental resource deletion
- Disaster recovery scenarios

The objective is to demonstrate how modern DevOps practices can improve deployment reliability, reduce operational risk, and enable faster recovery from failures.

---

# Business Problem

Modern application teams are expected to release software faster while maintaining high availability and reliability.

However, traditional deployment approaches introduce several operational challenges:

## Infrastructure Inconsistency

Manually created environments often become different over time because engineers apply changes differently across development, staging, and production environments.

This creates:

- Configuration drift
- Difficult troubleshooting
- Unpredictable deployments

## Manual Deployment Risk

Manual Kubernetes deployments can lead to:

- Incorrect configurations
- Human errors
- Slow release cycles
- Difficult rollback procedures

## Limited Disaster Recovery Capability

Without automated backups and recovery processes, organizations face:

- Long recovery times
- Data loss
- Extended application downtime

## Lack of Deployment Standardization

Organizations need repeatable processes that allow developers to deliver applications consistently across environments.

---

# Business Need

To overcome these challenges, organizations require a modern cloud-native delivery platform that provides:

- Automated infrastructure provisioning
- Version-controlled infrastructure changes
- Automated application delivery
- Continuous deployment processes
- Disaster recovery capabilities
- Improved operational visibility

This project addresses these requirements by implementing a complete GitOps-based Kubernetes platform.

---

# Project Objectives

The main objectives of this project are:

- Build a cloud-native application platform on Google Kubernetes Engine
- Implement Infrastructure as Code using Terraform
- Containerize applications using Docker
- Automate image building and delivery using GitHub Actions
- Implement GitOps deployment using Argo CD
- Create Kubernetes backup and recovery processes using Velero
- Validate disaster recovery through failure simulation
- Reduce deployment complexity and operational risk

---

# Solution Overview

The solution combines multiple DevOps practices into a single automated workflow.

The platform consists of three major stages:

---

# Stage 1 — Infrastructure Provisioning & Application Containerization

## Objective

Create a complete cloud foundation and prepare the application for deployment on Kubernetes.

## Why This Stage Is Required

Before applications can run in Kubernetes, the required infrastructure must exist.

Manual infrastructure creation creates several problems:

- Environment inconsistency
- Difficult reproduction
- Lack of version control
- Increased deployment time

Infrastructure as Code solves this problem by allowing infrastructure to be created automatically using repeatable configuration files.

---

# Stage 1 Architecture Components

The infrastructure layer contains:

| Component | Purpose |
|---|---|
| Terraform | Infrastructure provisioning |
| Google Kubernetes Engine (GKE) | Container orchestration platform |
| Google Cloud VPC | Network foundation |
| Google Artifact Registry | Container image storage |
| IAM Service Accounts | Secure resource access |
| Docker | Application containerization |

---

# Architecture Overview
![Achitecturela Diagram]()

### Step 2: Provision GKE with Terraform
## Why Terraform?

Terraform was selected because it provides Infrastructure as Code capabilities.
Instead of manually creating cloud resources, the entire infrastructure is defined using configuration files.
Benefits:
- Repeatable deployments
- Version-controlled infrastructure
- Reduced human error
- Easier disaster recovery
- Consistent environments
![Terraform Deployment](https://github.com/smogalloyubio/GoogleCloud-Disaster-Recovery-project-/blob/main/picture/Screenshot%202026-01-24%20at%2011.47.27.png)

## What Terraform Provisions
Once applied, Terraform automatically creates the following cloud resources:
- Google Kubernetes Engine (GKE) cluster
- Networking components (VPC, subnets, routing)
- IAM roles and service accounts required for cluster operation
  
 ![Terraform  apply command](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-24%20at%2012.18.12.png):**
---
1. Navigate to the Terraform directory:
   ```
   
    cd terraform directory
    terraform init
    terraform plan
    terraform  apply 
    sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
    wget -O- https://apt.releases.hashicorp.com/gpg | \
    gpg --dearmor | \
    sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
    https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
    sudo tee /etc/apt/sources.list.d/hashicorp.list
    sudo apt-get update && sudo apt-get install terraform
  ```
```
![Terraform  modoles](https://github.com/smogalloyubio/Googlecloud-Disaster-project-01/blob/main/picture/Screenshot%202026-01-24%20at%2012.25.09.png)
--- 



---

# Stage 2 — CI/CD Automation & GitOps Deployment:

# Objective
The objective of Stage 2 is to automate the application delivery process by implementing:

- Continuous Integration using GitHub Actions
- Container image build automation
- Image publishing to Artifact Registry
- Kubernetes deployment automation
- GitOps-based application synchronization using Argo CD
---

# Why This Stage Is Required
Traditional deployment methods require engineers to manually:

- Build application images
- Upload container images
- Modify Kubernetes YAML files
- Apply Kubernetes resources
- Verify deployments

This approach introduces operational risks:

- Human configuration mistakes
- Slow deployment cycles
- Environment differences
- Difficult rollback processes

A CI/CD and GitOps approach provides:

- Automated application delivery
- Version-controlled deployments
- Deployment traceability
- Faster release cycles
- Improved reliability

---
#Gitaction workflow  follow this process:
- Checks out the latest application source code from GitHub
- Builds a Docker image for the web application
- Tags the image with a version for traceability
- Authenticates securely with Google Cloud
- Pushes the image to Google Artifact Registry

**![Gitaction pipeline](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-24%20at%2011.12.05.png)**


## google cloud artifact registry 
the docker image  store in artifact registry 
![artifact registry](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-24%20at%2011.11.50.png)


![Artifact  registry image](https://github.com/smogalloyubio/Googlecloud-Disaster-project-01/blob/main/picture/Screenshot%202026-01-24%20at%2013.42.09.png)
---


## Step 4: Kubernetes Cluster Configuration and Manifests
After provisioning the Kubernetes cluster using Terraform, the next step was to configure the application workloads using Kubernetes manifests.

![Google kubernstes cluster](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-24%20at%2012.33.10.png)
---

# Step 5 — Install and Configure Argo CD GitOps Controller

## Objective

After deploying the Kubernetes cluster and preparing the application manifests, the next step is to implement a GitOps-based deployment workflow using Argo CD.
Argo CD is responsible for continuously monitoring the Kubernetes manifests stored in GitHub and ensuring that the actual state of the GKE cluster always matches the desired state defined in the repository.
This removes the need for manual Kubernetes deployments and provides an automated, reliable, and auditable application delivery process.

---

## Why Argo CD Was Selected
Although this works, it introduces operational challenges:
* Manual deployment processes
* Configuration drift between environments
* Limited deployment visibility
* Increased risk of human error
* Difficult rollback procedures

Argo CD solves these challenges by implementing GitOps principles.
With GitOps:
* Git becomes the single source of truth
* Every deployment change is version controlled
* Argo CD automatically detects configuration changes
* The Kubernetes cluster continuously reconciles with Git

---

# Install Argo CD on GKE

## Create Argo CD Namespace

Argo CD is deployed into its own dedicated namespace to isolate GitOps management components from application workloads.

```bash
kubectl create namespace argocd
```

---

## Deploy Argo CD Components
Install Argo CD using the official Kubernetes manifests:

```bash
kubectl apply \
-n argocd \
-f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
This deploys the required Argo CD components:
* Argo CD API Server
* Application Controller
* Repository Server
* Application Set Controller
* Redis component
---

## Verify Argo CD Installation
Check that all Argo CD pods are running:

```bash
kubectl get pods -n argocd
```
---
![Argocd Diagram](https://github.com/smogalloyubio/Googlecloud-Disaster-project-01/blob/main/picture/Screenshot%202026-01-24%20at%2012.35.26.png)
# Expose Argo CD Web Interface

By default, the Argo CD server is only accessible internally inside the Kubernetes cluster.

For external access, the service type is changed to LoadBalancer.

```bash
kubectl patch svc argocd-server \
-n argocd \
-p '{"spec":{"type":"LoadBalancer"}}'
```

Verify the service:

```bash
kubectl get svc -n argocd
```
---

# Retrieve Argo CD Administrator Password

Argo CD automatically creates an initial administrator password stored inside a Kubernetes secret.

Retrieve the password:

```bash
kubectl get secret argocd-initial-admin-secret \
-n argocd \
-o jsonpath="{.data.password}" | base64 -d
```
---

# Authenticate with Argo CD CLI

Login to the Argo CD server:

```
argocd login <ARGOCD_SERVER_IP> \
--username admin \
--password <PASSWORD> \
--insecure
```
---

# Connect Argo CD to GitHub Repository

The Kubernetes manifests repository is registered as the deployment source.

```bash
argocd repo add \
https://github.com/smogalloyubio/GoogleCloud-Disaster-Recovery-project.git
```
Argo CD can now monitor the repository and detect Kubernetes configuration changes.
---

# Create Argo CD Application
The application is created by linking:
* GitHub repository
* Kubernetes manifest directory
* Target GKE cluster
* Application namespace

```
argocd app create webapp \
--repo https://github.com/smogalloyubio/GoogleCloud-Disaster-Recovery-project.git \
--path apps \
--dest-server https://kubernetes.default.svc \
--dest-namespace dev
```

---
Enable automatic deployment whenever changes are committed to Git.

```

argocd app set webapp \
--sync-policy automated
```

Enable self-healing:

```bash
argocd app set webapp \
--self-heal
```

Enable automatic pruning of removed Kubernetes resources:

```bash
argocd app set webapp \
--auto-prune
```

---

# Deployment Verification

Check application synchronization status:

```
argocd app get webapp
```

Verify Kubernetes resources:

```bash
kubectl get all -n dev
```

---
![argocd cd](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-23%20at%2023.38.26.png)

---

### Step 6: Deploy Application via GitOps
- Push Kubernetes manifest changes to GitHub
- Argo CD automatically deploys to GKE
  
```
kubectl get pods -n namespace
kuebctl get all --all-namespace
kubectl get pods -n dev
#check  deployment of the  namespace
kubectl get pods -n  dev 
argocd app create webapp \
--repo  https://github.com/smogalloyubio/GoogleCloud-Disaster-Recovery-project.git
--path apps \
--dest-server https://kubernetes.default.svc \
--dest-namespace dev
argocd app sync apps 

```
 **![ argocd  deployment](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-23%20at%2023.45.03.png):**

---

### Step 7: Install and Configure Velero
---

# Step 7 — Install and Configure Velero Backup Solution

## Objective
The objective of this stage is to implement a Disaster Recovery (DR) solution for the Kubernetes application running on Google Kubernetes Engine (GKE).
Velero is deployed as the Kubernetes backup and recovery platform. It protects application workloads, Kubernetes resources, and cluster configurations by creating backups and storing them securely in Google Cloud Storage (GCS).
This enables the platform to recover from scenarios such as:
* Accidental namespace deletion
* Application configuration errors
* Kubernetes resource corruption
* Cluster failures
* Data loss incidents

---

# Why Velero Was Selected
Kubernetes is designed to maintain application availability, but it does not provide built-in disaster recovery capabilities.
If Kubernetes resources are accidentally deleted, the cluster fails, or application configuration is lost, the workloads cannot automatically be recovered without backups.
Velero solves this problem by providing:
* Kubernetes resource backup
* Namespace-level backup
* Cluster resource protection
* Restore capability
* Scheduled backup support
* Cloud storage integration
For this project, Velero uses **Google Cloud Storage (GCS)** as the backup storage backend.

---

# Disaster Recovery Architecture

The backup workflow follows this architecture:
---

# Install Velero CLI

Download the Velero client:

```bash
wget https://github.com/vmware-tanzu/velero/releases/download/v1.15.0/velero-v1.15.0-linux-amd64.tar.gz
```

Extract the package:

```bash
tar -xvf velero-v1.15.0-linux-amd64.tar.gz
```

Move Velero binary into the system path:

```bash
sudo mv velero-v1.15.0-linux-amd64/velero /usr/local/bin/
```

Verify installation:

```bash
velero version --client-only
```
---
# Configure Velero With Google Cloud Storage
Velero requires access to a GCS bucket where backup data will be stored.
The installation connects:
* Kubernetes cluster
* Velero controller
* Google Cloud Storage bucket
* Google Cloud authentication credentials
Install Velero:

```bash
velero install \
--provider gcp \
--plugins velero/velero-plugin-for-gcp:v1.8.0 \
--bucket <GCS_BUCKET_NAME> \
--secret-file ./credentials-velero
```
---
# Verify Velero Deployment
Check Velero components:

```bash
kubectl get pods -n velero
```
![Velero backup](https://github.com/smogalloyubio/Googlecloud-Disaster-project-01/blob/main/picture/Screenshot%202026-01-24%20at%2013.20.24.png)

Verify Velero configuration:

```bash
velero backup-location get
```

This confirms that Velero is successfully connected to Google Cloud Storage.
---

![Velero Installation and Backup Configuration](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-24%20at%2013.22.31.png)

---

# Step 8 — Create Kubernetes Application Backup

## Objective

Create a backup of the application environment to validate the disaster recovery process.

The backup contains Kubernetes resources required to restore the application, including:

* Deployments
* Services
* ConfigMaps
* Secrets
* Persistent volume information
* Namespace configuration

---

# Create Application Namespace Backup

Create a Velero backup:

```bash
velero backup create webapp-backup \
--include-namespaces dev
```

This creates a backup containing all Kubernetes resources inside the application namespace.

---

# Check Backup Status

View available backups:

```bash
velero backup get
```

Example:

```
NAME             STATUS

webapp-backup    Completed
```

Detailed backup information:

```bash
velero backup describe webapp-backup
```

This provides:

* Backup creation time
* Resources included
* Backup storage location
* Completion status

---

![Velero Backup Created](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-24%20at%2013.21.54.png)

---
![Velero deployment](https://github.com/smogalloyubio/Googlecloud-Disaster-project-01/blob/main/picture/Screenshot%202026-01-24%20at%2013.26.08.png)

# Backup Validation Result
---
**![velero backup](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-24%20at%2013.22.31.png):**


---

### Step 8: Backup Application Namespace

Create a namespace-scoped backup:

```bash
velero backup create netflix-backup --include-namespaces all-namespace
velero  backup  dscribe netflix-backup
velero  backup get

```

Check backup status:

```bash
velero backup get
```

![velero backup](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-24%20at%2013.21.54.png)



---

### Step 9: Disaster Simulation

* Delete the application namespace or entire cluster

```bash
kubectl delete namespace -all-namespace  dev  canary argocd
kubectl get namespace 
```

**![check  namespace](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-24%20at%2013.26.08.png):**

> Add screenshot showing namespace deletion

---

### Step 10: Restore from Backup

Restore the backup:

```bash
velero restore create --from-backup netflix-backup
```

Verify restore:

```bash
kubectl get all -n <APP_NAMESPACE>
```

**![retore namespace](https://github.com/smogalloyubio/02-Devops-project-NetflixClone-app/blob/main/picture/Screenshot%202026-01-24%20at%2013.36.05.png):**


---

## Disaster Recovery Validation
A disaster recovery test was performed to validate the reliability and resilience of the system.
- A full backup of the application namespace was created using Velero
- The application namespace (and cluster components) was intentionally deleted to simulate a failure scenario
- The system was restored using backups stored in Google Cloud Storage (GCS)
Post-Restore Verification
After the restore process, the following were confirmed:
- All pods were successfully recreated
- Services were restored and accessible
- The application returned to a fully functional state
- No data or configuration loss was observed
---
## Security Considerations

The project follows cloud security best practices to ensure a secure and controlled environment:
- IAM roles are configured using the principle of least privilege
- Service accounts are isolated and scoped per component
- Sensitive information and secrets are not stored in the Git repository
- GitOps provides a complete audit trail of all infrastructure and deployment changes
---
![storage bucket for velero backup](https://github.com/smogalloyubio/GoogleCloud-Disaster-Recovery-project-/blob/main/picture/Screenshot%202026-01-24%20at%2013.40.09.png)




