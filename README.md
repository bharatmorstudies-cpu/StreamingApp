# MERN StreamingApp - Orchestration & Deployment Architecture

This repository contains the complete containerized setup, CI/CD pipeline engine, and Kubernetes deployment configuration for the MERN Streaming Application.

## System Architecture Layout
1. **Source Code**: Managed on GitHub (Forked Repository).
2. **Continuous Integration**: Jenkins triggers automated Docker image compilation upon new code commits.
3. **Container Registry**: Compiled images are published to private Amazon ECR repositories.
4. **Orchestration**: Managed via an Amazon EKS Cluster.
5. **Package Management**: Automated via structured Helm Charts.

---

## 1. Container Engine Specs (Docker)
- **Frontend Container**: Multi-stage build leveraging Node.js for compilation and production-grade Nginx for high-performance static asset hosting.
- **Backend Container**: Node.js microservice optimized on a lightweight Alpine base runtime footprint.

## 2. CI/CD Architecture (Jenkins Pipeline)
The root Jenkinsfile maps out declarative automated stages:
- Checks out fresh branch changes.
- Authenticates programmatically against the Amazon ECR registry endpoint.
- Builds unique multi-architecture runtime container binaries tagged by pipeline build execution values.
- Publishes assets into regional private container image endpoints (p-south-1).

## 3. Kubernetes Infrastructure (Helm Engine)
Deployments are grouped and packaged inside a structured chart template tree:
- **Replica Configurations**: Configured with a default state scaling value of 2 pods across independent available subnets.
- **Frontend Service**: Network LoadBalancer distribution mapping external client web engine ports.
- **Backend Service**: ClusterIP internal distribution network layer ensuring secure container network boundaries.
