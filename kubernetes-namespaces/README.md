🎉 Kubernetes Cross-Namespace Communication Demo
A simple yet powerful demonstration of deploying applications in Kubernetes across multiple namespaces and understanding how services communicate cluster-wide using DNS and IP addresses.

📁 Repository Structure
create-cluster.yaml
Creates a multi-node Kind cluster with port mapping
namespace-creation.yaml
Creates namespace:
practise-namespace
name-space2.yaml
Creates namespace:
demo
deployment.yaml
Deploys a React frontend app (2 replicas)
service-apache.yaml
Exposes the app via a NodePort service on port
30008

🔧 Prerequisites
Before you begin, ensure you have the following installed:

Docker
kubectl
kind
🚀 Getting Started
1. Create a Local Kubernetes Cluster
bash

kind create cluster --config=create-cluster.yaml
This creates a cluster with: 

1 Control-plane node
2 Worker nodes
Host port 30008 mapped to control-plane node
2. Create Namespaces
bash

kubectl apply -f namespace-creation.yaml
kubectl apply -f name-space2.yaml
Creates two custom namespaces:

practise-namespace
demo
3. Deploy Application
bash



kubectl apply -f deployment.yaml
Deploys a React frontend application using the image:
ziasaeeditgeek/three-tier-react-frontend:latest.

⚠️ By default, this is deployed in the default namespace . 

4. Expose as Service
bash



kubectl apply -f service-apache.yaml
Exposes the app as a NodePort service on port 30008.

You can access the app at:
🔗 http://localhost:30008

🌐 Cross-Namespace Communication
This demo helps understand how pods from one namespace interact with services in another.

✅ Success: Using Fully Qualified DNS Name
To reach a service in a different namespace, use:




<service-name>.<namespace>.svc.cluster.local
Example:

bash



curl http://react-service.default.svc.cluster.local
❌ Failure: Using Only Service Name
Trying this will fail unless the pod is also in the same namespace:

bash



curl react-service
💡 Services are scoped to their own namespace by default. 

🧪 Test Communication Between Namespaces
Try these advanced tests:

Deploy a utility pod (like busybox or curlimages/curl) in practise-namespace or demo.
Try curling the service in default using both:
Pod IP address ✅
react-service.default.svc.cluster.local ✅
react-service ❌
📋 Summary Table
Create cluster
kind create cluster --config=create-cluster.yaml
Apply namespaces
kubectl apply -f namespace-creation.yaml
and
name-space2.yaml
Deploy app
kubectl apply -f deployment.yaml
Expose service
kubectl apply -f service-apache.yaml
Access app
http://localhost:30008
Curl across namespaces
curl http://react-service.default.svc.cluster.local

🧑‍💻 Want to Extend?
Here are some ideas:

Add a backend service in a separate namespace.
Use Network Policies to restrict traffic between namespaces.
Automate testing with scripts or CI/CD pipelines.
🙌 Contributing
Contributions welcome! Feel free to fork this repo, open issues, or submit pull requests.
