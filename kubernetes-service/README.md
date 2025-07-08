# Kind Kubernetes Cluster with NGINX Deployment

This repository sets up a local Kubernetes cluster using [Kind (Kubernetes IN Docker)](https://kind.sigs.k8s.io/), deploys an NGINX application, and exposes it using a `NodePort` service.

---

## 📁 Project Structure

.
├── kind-cluster.yaml # Cluster config for Kind
├── deployment.yaml # NGINX Deployment manifest
├── service.yaml # NodePort Service for NGINX
├── lb.yaml # LoadBalancer Service (not used in Kind)
└── README.md # Project documentation

yaml
Copy
Edit

---

## ⚙️ Prerequisites

- Docker installed and running
- `kubectl` installed
- [Kind](https://kind.sigs.k8s.io/) installed

---

## 🚀 Steps to Use

### 1. Create a Kind Cluster

```bash
kind create cluster --config kind-cluster.yaml
This creates a multi-node cluster (1 control-plane, 2 workers) and maps port 30001 on the host to the NGINX service inside the cluster.

2. Deploy the NGINX App
bash
Copy
Edit
kubectl apply -f deployment.yaml
This creates a deployment with 5 NGINX pods labeled run: nginx-pod.

3. Expose the Deployment via NodePort
bash
Copy
Edit
kubectl apply -f service.yaml
This creates a NodePort service on port 30001 of the host machine, allowing access to NGINX externally via:

arduino
Copy
Edit
http://localhost:30001
4. (Optional) LoadBalancer Service
The lb.yaml file defines a LoadBalancer type service. However, Kind does not support external LoadBalancers by default, so this file is not used unless you set up a local load balancer like MetalLB.

To apply it anyway:

bash
Copy
Edit
kubectl apply -f lb.yaml
📌 Notes
Ensure the labels used in the deployment.yaml match those in the service.yaml. In this case, the label is run: nginx-pod.

Kind supports NodePort services but not real external LoadBalancers.
