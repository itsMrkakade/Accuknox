# Accuknox
* Deploy a local k8s cluster (using minikube, k3s, or anything else) and deploy the
DVWA application. Showcase/demo 3 attack surfaces as mentioned in its
documentation.
# DVWA Kubernetes Deployment

This repository contains Kubernetes manifests and instructions for deploying the Damn Vulnerable Web Application (DVWA) on a local Kubernetes cluster using Minikube.

## Prerequisites

- Minikube
- kubectl

## Setup

1. Start Minikube:

    ```bash
    minikube start --memory=4096 --cpus=2
    ```

2. Apply the Kubernetes manifests:

    ```bash
    kubectl apply -f deployment.yaml
    kubectl apply -f service.yaml
    ```

3. Access DVWA:

    Get the Minikube IP:

    ```bash
    minikube ip
    ```

    Access DVWA at `http://<minikube-ip>:30001`.

## Attack Surfaces Demonstration

### SQL Injection

1. Navigate to `Vulnerabilities -> SQL Injection`.
2. Perform an SQL Injection using: `1' OR '1'='1`.

### Cross-Site Scripting (XSS)

1. Navigate to `Vulnerabilities -> XSS (Reflected)`.
2. Perform an XSS Attack using: `<script>alert('XSS')</script>`.

### Command Injection

1. Navigate to `Vulnerabilities -> Command Injection`.
2. Perform a Command Injection using: `8.8.8.8 && ls`.

## Cleanup

To clean up the resources:

```bash
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
minikube stop
minikube delete


### Upload to GitHub

1. Initialize a Git repository:

```bash
git init
2.Add the files and commit:
```bash
git add .
git commit -m "Initial commit"

3.Create a new repository on GitHub and push the local repository:
```bash

git remote add origin https://github.com/itsMrkakade/dvwa-k8s.git
git push -u origin master
