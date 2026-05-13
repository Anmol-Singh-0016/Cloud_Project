# DevOps-MasterPiece
## Production-Grade CI/CD Pipeline with DevSecOps & GitOps

---

# 🚀 Project Overview

DevOps-MasterPiece is a Production-Grade DevSecOps CI/CD Pipeline project that automates the complete software delivery lifecycle using modern DevOps, DevSecOps, and GitOps tools.

The project demonstrates how organizations can build secure, scalable, automated, and production-ready deployment workflows using Jenkins, ArgoCD, Kubernetes, Docker, SonarQube, Trivy, Prometheus, Grafana, Hashicorp Vault, and AWS services.

This pipeline follows:

- Continuous Integration (CI)
- Continuous Deployment (CD)
- DevSecOps Best Practices
- GitOps Deployment Methodology
- Infrastructure Monitoring & Alerting

---

# 📌 Features

- Automated CI/CD Pipeline
- GitOps-based Deployment
- Docker Containerization
- Kubernetes Deployment using EKS
- SonarQube Code Quality Analysis
- Trivy Vulnerability Scanning
- Artifact Management using JFrog Artifactory
- Slack Notifications
- Monitoring using Prometheus & Grafana
- Secret Management using Hashicorp Vault
- Pull Request-based Production Deployment

---

# 🏗️ Architecture Flow

```text
Developer Pushes Code
        ↓
GitHub Repository
        ↓
GitHub Webhook
        ↓
Jenkins Pipeline Triggered
        ↓
Maven Build + JUnit Testing
        ↓
SonarQube Analysis + Quality Gate
        ↓
Artifacts Upload to JFrog Artifactory
        ↓
Docker Image Build
        ↓
Trivy Security Scan
        ↓
Upload Reports to AWS S3
        ↓
Push Docker Image to DockerHub
        ↓
Update Kubernetes Manifest Repo
        ↓
Create Pull Request
        ↓
Manual Approval & Merge
        ↓
ArgoCD Detects Changes
        ↓
Deploy Application to EKS
        ↓
Prometheus & Grafana Monitoring
        ↓
Slack Notifications
```

---

# 🛠️ Tools & Technologies Used

| Category | Tools |
|---|---|
| Version Control | Git, GitHub |
| CI/CD | Jenkins, ArgoCD |
| Build Tools | Maven, JUnit |
| Security | SonarQube, Trivy, Vault |
| Containerization | Docker |
| Orchestration | Kubernetes (EKS), Helm |
| Artifact Management | JFrog Artifactory |
| Cloud Services | AWS EC2, AWS S3, AWS EKS |
| Monitoring | Prometheus, Grafana |
| Notifications | Slack |
| Infrastructure as Code | Terraform |

---

# ☁️ AWS Infrastructure Used

| Server | Purpose | Instance Type |
|---|---|---|
| Jenkins Server | Jenkins, Docker, Trivy, Terraform | t2.large |
| SonarQube Server | SonarQube + Vault | t2.medium |
| Artifactory Server | JFrog Artifactory | t2.medium |
| EKS Worker Nodes | Kubernetes Cluster | t3.medium |

---

# 📂 Project Structure

```text
DevOps-MasterPiece/
│
├── Application-Code/
├── Dockerfile
├── Jenkinsfile
├── kubernetes-manifests/
├── terraform/
├── monitoring/
├── sonar-project.properties
└── README.md
```

---

# ⚙️ Prerequisites

Install the following tools before starting:

- Java JDK
- Git
- GitHub CLI
- Jenkins
- Docker
- Trivy
- AWS CLI
- Terraform
- kubectl
- Helm
- SonarQube
- Hashicorp Vault
- JFrog Artifactory
- Slack

---

# 🔥 Step-by-Step Implementation

# Step 1: Install Java JDK

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```

---

# Step 2: Install Jenkins

## Add Jenkins Repository

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
```

## Install Jenkins

```bash
sudo apt update
sudo apt install jenkins -y
```

## Start Jenkins

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

---

# Step 3: Install Docker

```bash
sudo apt install docker.io -y
```

## Add User to Docker Group

```bash
sudo usermod -aG docker $USER
sudo usermod -aG docker jenkins
```

## Restart Docker

```bash
sudo systemctl restart docker
```

---

# Step 4: Install Trivy

```bash
sudo apt-get install wget apt-transport-https gnupg lsb-release -y
```

```bash
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
```

```bash
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | \
sudo tee -a /etc/apt/sources.list.d/trivy.list
```

```bash
sudo apt-get update
sudo apt-get install trivy -y
```

---

# Step 5: Install AWS CLI

```bash
sudo apt install unzip curl -y
```

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

```bash
unzip awscliv2.zip
sudo ./aws/install
```

## Configure AWS CLI

```bash
aws configure
```

---

# Step 6: Install GitHub CLI

```bash
type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y)
```

```bash
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | \
sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
```

```bash
sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg
```

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | \
sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
```

```bash
sudo apt update
sudo apt install gh -y
```

---

# Step 7: Install Terraform

```bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common wget
```

```bash
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
```

```bash
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```

```bash
sudo apt update
sudo apt install terraform -y
```

---

# Step 8: Install SonarQube

## Install Docker First

```bash
sudo apt update
sudo apt install docker.io -y
```

## Run SonarQube Container

```bash
sudo docker run -d -p 9000:9000 --name sonarqube sonarqube
```

## Access SonarQube

```text
http://<SERVER-IP>:9000
```

Default Credentials:

```text
Username: admin
Password: admin
```

---

# Step 9: Install Hashicorp Vault

```bash
sudo curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```

```bash
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```

```bash
sudo apt update
sudo apt install vault -y
```

---

# Step 10: Configure Vault

## Edit Vault Configuration

```bash
sudo nano /etc/vault.d/vault.hcl
```

## Add Configuration

```hcl
storage "raft" {
  path    = "/opt/vault/data"
  node_id = "raft_node_1"
}

listener "tcp" {
  address     = "0.0.0.0:8200"
  tls_disable = 1
}

api_addr = "http://127.0.0.1:8200"
cluster_addr = "https://127.0.0.1:8201"
ui = true
```

## Restart Vault

```bash
sudo systemctl restart vault
```

## Initialize Vault

```bash
export VAULT_ADDR='http://127.0.0.1:8200'
```

```bash
vault operator init
```

## Unseal Vault

```bash
vault operator unseal
```

## Login to Vault

```bash
vault login <ROOT_TOKEN>
```

---

# Step 11: Install JFrog Artifactory

```bash
sudo apt update
sudo apt install docker.io -y
```

## Pull Artifactory Image

```bash
sudo docker pull docker.bintray.io/jfrog/artifactory-oss:latest
```

## Create Directory

```bash
sudo mkdir -p /jfrog/artifactory
sudo chown -R 1030 /jfrog/
```

## Run Artifactory Container

```bash
sudo docker run --name artifactory -d -p 8081:8081 -p 8082:8082 \
-v /jfrog/artifactory:/var/opt/jfrog/artifactory \
docker.bintray.io/jfrog/artifactory-oss:latest
```

---

# Step 12: Create EKS Cluster using Terraform

## Initialize Terraform

```bash
terraform init
```

## Validate Configuration

```bash
terraform validate
```

## Plan Infrastructure

```bash
terraform plan
```

## Create Infrastructure

```bash
terraform apply
```

## Configure kubectl

```bash
aws eks --region <REGION> update-kubeconfig --name <CLUSTER_NAME>
```

---

# Step 13: Install ArgoCD

## Create Namespace

```bash
kubectl create namespace argocd
```

## Install ArgoCD

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Change Service Type to NodePort

```bash
kubectl -n argocd edit svc argocd-server
```

---

# Step 14: Install Helm

```bash
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
```

```bash
sudo apt-get install apt-transport-https --yes
```

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
```

```bash
sudo apt-get update
sudo apt-get install helm -y
```

---

# Step 15: Install Prometheus & Grafana

## Add Helm Repositories

```bash
helm repo add stable https://charts.helm.sh/stable
```

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```

## Create Namespace

```bash
kubectl create namespace prometheus
```

## Install Monitoring Stack

```bash
helm install stable prometheus-community/kube-prometheus-stack -n prometheus
```

## Verify Pods

```bash
kubectl get pods -n prometheus
```

## Verify Services

```bash
kubectl get svc -n prometheus
```

---

# 🔐 Jenkins Integrations

# Integrate SonarQube with Jenkins

- Manage Jenkins → Configure System
- Add SonarQube Server
- Add Authentication Token

---

# Integrate Vault with Jenkins

- Install Vault Plugin
- Configure Vault URL
- Add AppRole Credentials

---

# Integrate DockerHub with Jenkins

- Add DockerHub Credentials
- Configure Docker Login

---

# Integrate Slack with Jenkins

- Install Slack Plugin
- Add Slack Token
- Configure Channel Name

---

# 📜 Jenkins Pipeline Stages

| Stage | Description |
|---|---|
| Git Checkout | Clone source code |
| Build | Build application using Maven |
| JUnit Test | Execute unit tests |
| SonarQube Analysis | Scan code quality |
| Quality Gate | Validate security standards |
| Artifactory Upload | Store artifacts |
| Docker Build | Build Docker image |
| Trivy Scan | Scan image vulnerabilities |
| S3 Upload | Upload reports to AWS S3 |
| Docker Push | Push image to DockerHub |
| Manifest Update | Update Kubernetes manifests |
| Pull Request | Create PR for deployment |
| ArgoCD Deploy | Deploy app to EKS |
| Slack Notification | Send alerts |

---

# 📄 Sample Jenkinsfile

```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/project/repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube-server') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t app:latest .'
            }
        }

        stage('Trivy Scan') {
            steps {
                sh 'trivy image app:latest'
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push app:latest'
            }
        }
    }
}
```

---

# 📊 Monitoring

## Prometheus Monitors

- Kubernetes Cluster
- Nodes
- Pods
- Containers
- CPU Usage
- Memory Usage

## Grafana Dashboards

- Infrastructure Metrics
- Kubernetes Health
- Resource Utilization
- Application Monitoring

---

# 🔔 Slack Notifications

Slack sends notifications for:

- Build Success
- Build Failure
- Deployment Success
- Deployment Failure
- ArgoCD Sync Status

---

# 🔒 Security Best Practices Implemented

- Secrets stored in Hashicorp Vault
- Docker image vulnerability scanning using Trivy
- Code quality validation using SonarQube
- Pull Request approval before production deployment
- GitOps-based deployment strategy
- Kubernetes deployment automation

---

# 📈 Project Outcomes

- Fully Automated CI/CD Pipeline
- Production-like DevSecOps Workflow
- Secure Kubernetes Deployment
- Automated Vulnerability Scanning
- Real-Time Monitoring & Alerts
- Faster Software Delivery
- Reduced Manual Effort
- Improved Deployment Reliability

---

# 🚀 Future Enhancements

- Blue-Green Deployment
- Canary Deployment
- ELK Stack Logging
- Service Mesh using Istio
- AI-based Monitoring
- Multi-Cloud Deployment
- Auto Scaling

---

# 📷 Screenshots Section

Add screenshots in the following sequence:

1. Jenkins Dashboard
2. Jenkins Pipeline Output
3. SonarQube Dashboard
4. Artifactory Dashboard
5. DockerHub Images
6. Trivy Report
7. Pull Request Screenshot
8. ArgoCD Dashboard
9. Kubernetes Pods
10. Grafana Dashboard
11. Prometheus Dashboard
12. Slack Notifications

---

# ✅ Conclusion

This project demonstrates a complete Production-Grade DevSecOps CI/CD Pipeline integrated with GitOps principles.

By using Jenkins for Continuous Integration and ArgoCD for Continuous Deployment, the project automates the entire software delivery lifecycle securely and efficiently.

The integration of SonarQube, Trivy, Hashicorp Vault, Prometheus, Grafana, Docker, Kubernetes, and AWS services makes the system highly scalable, secure, observable, and production-ready.

This project successfully showcases how modern DevOps practices can improve deployment reliability, infrastructure automation, and software delivery speed in enterprise environments.

