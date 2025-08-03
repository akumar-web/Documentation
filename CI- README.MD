# Note: This project is a fork of opentelemetry-demo. Thanks to the team and contributors for opensourcing this wonderful demo project. Definitely one of the best on internet.

# This project has multiple microservice running in EKS Cluster  .I just created CI CD pipeline for one of the microservice named product-catalog to present my test infront of you.



# Steps -:

1. Implement continuous integration for the project
2. GitHub Actions setup for a micro service of the project
3. CI/CD for the project
4. GitHub Action with Argo CD for end to end CI/CD



*** Complete Explanation of the CI.YAML 

# 📦 Product Catalog Service

This repository contains the source code and CI/CD configuration for the **Product Catalog Service**, built in Go and deployed via Docker and Kubernetes. GitHub Actions is used to automate building, testing, linting, containerization, and deployment.

---

## 🚀 CI/CD Workflow Overview

The GitHub Actions pipeline is triggered on **pull requests to the `main` branch** and consists of the following jobs:

- **Build & Test**
- **Code Quality (Linting)**
- **Docker Build & Push**
- **Kubernetes Manifest Update**

---

## 🔧 Workflow Jobs

### 1. 🧱 Build & Unit Test (`build` job)

Compiles the Go application and runs unit tests to ensure code correctness.

#### Steps:
- **Checkout Code**
- **Setup Go 1.22**
- **Build the Binary**  
  Compiles `main.go` into `product-catalog-service`.
- **Run Unit Tests**  
  Runs all unit tests in the project.

```bash
go mod download
go build -o product-catalog-service main.go
go test ./...


**** 2. Code Quality Check (code-quality job)
Uses golangci-lint to enforce code style and detect potential issues.

Steps:
Checkout Code

Setup Go

Run Linter
Executes lint checks on the source directory.

**** 3. 🐳 Docker Build & Push (docker job)
Builds a Docker image for the service and pushes it to Docker Hub.

Steps:
Setup Docker Buildx

Login to Docker Hub

Build & Push Image
Tags include:

product-catalog:<github.run_id>

product-catalog:latest (optional)

**** 4. ☸️ Kubernetes Manifest Update (updatek8s job)
Updates the Kubernetes deployment YAML with the new Docker image tag.

Steps:
Checkout Code with Write Access

Update Image Tag in Manifest

Commit & Push Change
Auto-commits back to the repository (optionally to main).

**** 5. Secrets Used

DOCKER_USERNAME     	Docker Hub username
DOCKER_TOKEN	        Docker Hub access token
GITHUB_TOKEN	        GitHub Actions token (auto-injected)

**** Note -: These secrets are created in github insdie repository settings under Secrets and Variables.

Pipeline Link to verify CI working end to end till updating K8S Manifest in repostiory
https://github.com/akumar-web/CI-CD-DEMO/actions/runs/16699870796
