Project 2 – Deploying Microservices on Kubernetes (EKS) + CI/CD with GitHub Actions
 Overview

In this project, I redeployed the same microservices as in week4 / project 1, but this time using a cloud‑native, Kubernetes‑based architecture, combined with a full CI/CD pipeline.

 Goals

1. Containerize and deploy microservices on Kubernetes

Deploy Redis and PostgreSQL as Deployments

Deploy vote, result, and worker services with Deployments + Services

Install and configure NGINX Ingress Controller

Set up GitHub Actions for automated builds and deployments

 2. Kubernetes Deployments
Cluster structure

Namespace: personal namespace inside a shared cluster

Deployments: vote, result, worker, redis, postgres

Services: ClusterIP for internal communication, exposed via Ingress

Ingress routes:

/vote → vote-service

/result → result-service

Microservices communicate using internal DNS:

redis-service.default.svc.cluster.local

No more hardcoded IPs.

 3. CI/CD Pipeline (GitHub Actions)
Pipeline responsibilities:

Build Docker images

Push to Docker Hub

Configure AWS credentials

Update kubeconfig

Apply Kubernetes manifests automatically

Example workflow steps:

- name: Configure AWS Credentials
  uses: aws-actions/configure-aws-credentials@v1


- name: Update kubeconfig
  run: eksctl utils write-kubeconfig --cluster <cluster-name>


- name: Apply Manifests
  run: kubectl apply -f K8s/
 Validation & Testing

kubectl get pods to verify all pods are running

kubectl get ingress to retrieve the public endpoint

Access /vote and /result via the Ingress URL

 Key Learnings

Containerization best practices (multi‑arch, Docker Compose, image optimization)

Infrastructure as Code with Terraform (VPC design, EC2 provisioning, remote state)

Configuration management with Ansible (SSH tunneling, automation)

Kubernetes fundamentals (Deployments, Services, DNS, Ingress)

Building cloud‑native CI/CD pipelines with GitHub Actions

Full DevOps lifecycle: build → test → deploy → automate
