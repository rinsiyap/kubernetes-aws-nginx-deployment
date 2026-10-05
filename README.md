# Kubernetes AWS NGINX Deployment

## Project Overview

This project demonstrates the deployment and exposure of a containerized NGINX web application using Kubernetes on an AWS EC2 Ubuntu instance.

The project covers Kubernetes cluster setup, container runtime configuration, networking, application deployment, service exposure, scaling, and application verification.

## Architecture

AWS EC2 Ubuntu
        |
        v
Kubernetes Cluster
        |
        +-- Flannel CNI
        |
        +-- NGINX Deployment
                |
                +-- NGINX Pod 1
                |
                +-- NGINX Pod 2
                        |
                        v
                  NGINX Service
                    NodePort 30080
                        |
                        v
                  Web Browser

## Environment

- Cloud Platform: AWS EC2
- Operating System: Ubuntu
- Kubernetes: v1.34.12
- Container Runtime: containerd 2.2.2
- Kubernetes Networking: Flannel
- Application: NGINX Alpine
- Kubernetes Service: NodePort
- Application Port: 80
- NodePort: 30080

## Task 1 - Kubernetes Setup

The Kubernetes environment was configured on an AWS EC2 Ubuntu instance.

### Components Installed

- containerd
- kubeadm
- kubelet
- kubectl
- Flannel CNI

### Cluster Configuration

The cluster was initialized using kubeadm with the pod network CIDR:

10.244.0.0/16

Flannel was used as the Container Network Interface.

The control-plane taint was removed because this was a single-node learning environment.

### Verification

The Kubernetes node was successfully verified as Ready.

System components including:

- CoreDNS
- kube-apiserver
- kube-controller-manager
- kube-scheduler
- etcd
- kube-proxy
- Flannel

were verified as Running.

## Task 2 - Application Deployment

An NGINX container was deployed using a Kubernetes Deployment.

### Deployment

The application was initially deployed with one replica.

The Deployment configuration is available in:

deployment.yaml

### Service

A NodePort Service was created to expose the NGINX application outside the Kubernetes cluster.

The service configuration is available in:

service.yaml

The application was exposed using:

NodePort: 30080

### Application Testing

The application was tested using:

curl http://localhost:30080

The NGINX welcome page was successfully returned.

The application was also accessed externally through the AWS EC2 public IP using:

http://<EC2-PUBLIC-IP>:30080

## Scaling

The application was scaled from one replica to two replicas.

Command:

kubectl scale deployment nginx-deployment --replicas=2

Both replicas were successfully verified as Running.

The Kubernetes Service showed both Pod endpoints.

## Logs

NGINX application logs were reviewed using:

kubectl logs <pod-name>

HTTP requests returned status code 200, confirming successful application requests.

## Testing and Verification

The following Kubernetes resources were verified:

- Kubernetes node status
- Deployment status
- Pod status
- Service configuration
- Service endpoints
- Application accessibility
- Replica scaling
- Application logs

## Real-World Use Cases

The concepts demonstrated in this project are applicable to:

- Microservice deployment
- Web application hosting
- Container orchestration
- Application scaling
- High availability
- Service discovery
- Cloud-native application deployment
- DevOps automation

## Skills Demonstrated

- AWS EC2
- Linux
- Kubernetes
- kubectl
- kubeadm
- kubelet
- containerd
- Kubernetes Networking
- Flannel
- Docker/Container concepts
- NGINX
- YAML
- NodePort Services
- Application Scaling
- Troubleshooting

## Project Result

Successfully deployed and exposed an NGINX application on a Kubernetes cluster running on AWS EC2.

The application was accessible through a Kubernetes NodePort and successfully scaled from one to two replicas.

## Note

This project was implemented as a learning/practical environment using a small AWS EC2 instance.
