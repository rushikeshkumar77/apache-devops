# 🚀 Apache DevOps on Kubernetes

This repository contains a complete Kubernetes deployment of Apache HTTP Server with **HPA (Horizontal Pod Autoscaler)**, **VPA (Vertical Pod Autoscaler)**, and **RBAC (Role-Based Access Control)**.

## 📁 Repository Structure
## 🚀 Quick Deploy

```bash
# 1. Create namespace
kubectl apply -f namespace.yml

# 2. Deploy Apache
kubectl apply -f deployment.yml
kubectl apply -f service.yml

# 3. Setup Autoscaling
kubectl apply -f hpa.yml
kubectl apply -f vpa.yml

# 4. Setup RBAC
kubectl apply -f serviceaccount.yml
kubectl apply -f role.yml
kubectl apply -f rolebinding.yml

# 5. Verify deployment
kubectl get all -n apache
kubectl get hpa,vpa -n apache
# Check HPA status
kubectl get hpa -n apache

# Check VPA recommendations
kubectl describe vpa apache-vpa -n apache

# Check pod resource usage
kubectl top pods -n apache

# Check RBAC
kubectl auth can-i list pods --as=system:serviceaccount:apache:apache-sa -n apache

# Port-forward the service
kubectl port-forward -n apache svc/apache-service 8080:80

# In another terminal, generate load
while true; do curl -s http://localhost:8080 > /dev/null; done

# Watch HPA scale
kubectl get hpa -n apache --watch
exit
