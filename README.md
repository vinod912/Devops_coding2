# Devops_coding2
# Kubernetes Autoscaling for Spring Boot Frontend Application

## Overview
This project demonstrates how to deploy and autoscale a Java Spring Boot frontend application on Kubernetes, while connecting to an external RDS database.

## Architecture
- The frontend app runs inside Kubernetes pods managed by a - Deployment.
- The backend database is an external AWS RDS instance, accessed via environment variables.
- Horizontal Pod Autoscaler (HPA) scales the number of pods based on CPU utilization to handle varying load.

## Files
- springboot-deployment.yaml: Kubernetes Deployment manifest for the Spring Boot app.
- springboot-hpa.yaml: Kubernetes Horizontal Pod Autoscaler manifest to scale pods between 2 and 5 replicas based on 70% average CPU utilization.

## Prerequisites
- Kubernetes cluster (EKS, GKE, AKS, or on-prem) with Metrics Server installed.
- kubectl configured to interact with your cluster.
- Docker image of the Spring Boot app pushed to a container registry accessible by the cluster.
- AWS RDS instance running your database, with network access configured for the Kubernetes cluster.

## How to Deploy
 ### Create name space 
 kubectl create namespace springboot
 ### Deploy the Spring Boot application:
kubectl apply -f springboot-deployment.yaml
 ### Deploy the Horizontal Pod Autoscaler:
kubectl apply -f springboot-hpa.yaml
## Verify pods and HPA:
kubectl get pods -n springboot

kubectl get hpa -n springboot
## Autoscaling Threshold
- The HPA monitors CPU usage across pods.
- When average CPU utilization exceeds 70%, the HPA scales up the number of pods (up to 5 replicas).
- When CPU usage drops below threshold, pods are scaled down (minimum 2 replicas).
- This ensures your application can handle higher traffic smoothly.

