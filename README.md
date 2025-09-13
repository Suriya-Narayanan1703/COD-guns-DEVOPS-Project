# COD-guns-DEVOPS-Project
Interactive Call of Duty Guns List – A static HTML web application displaying popular COD weapons. Hovering over each gun reveals detailed stats including range, damage, fire rate, and type. Ideal for gamers, fans, and web development learning demos.


Static website project containerized with Docker, demonstrating basic Dockerfile usage, local container builds, and pushing web assets to GitHub. Includes step-by-step learning of Git commands and Docker fundamentals for DevOps workflow foundation.


# COD Guns Static Website - Dockerized Project

## Project Overview

This project hosts a simple static HTML website showcasing a Call of Duty guns list. The main goal of this repository is to demonstrate:

- Version control using Git and GitHub
- Containerization of a static website with Docker
- Building and running Docker images locally

It serves as a foundational project to understand essential DevOps practices including source code management and container workflow, preparing for later steps like Kubernetes deployment, Helm charts, and CI/CD pipelines.

---
Step 3: Deploy and Expose Static Website on Minikube Kubernetes
Objective
Deploy your static website as a Kubernetes Deployment.

Expose it via a Kubernetes Service of type NodePort.

Access the app through Minikube IP and NodePort.

Commands & Process
1. Build and Tag Docker Image (if local)
bash
docker build -t cod-guns-web:latest .
Fix any tag typos:

bash
docker tag cod-guns-web:lastest cod-guns-web:latest
docker rmi cod-guns-web:lastest
2. Load Image into Minikube (Docker driver does not share local images)
bash
minikube image load cod-guns-web:latest
3. Apply Deployment Manifest
Ensure your deployment YAML uses this image and set imagePullPolicy: IfNotPresent:

bash
kubectl apply -f deployment.yaml
4. Apply Service Manifest
Expose the deployment via NodePort on fixed port (e.g., 30008):

bash
kubectl apply -f service.yaml
5. Verify Pods and Services
bash
kubectl get pods
kubectl get svc
Common Issues & Solutions
Issue: Pod stuck in ImagePullBackOff
Reason: Kubernetes cannot pull the image because it’s not in a remote registry or image tag mismatch.

Solution:

Ensure correct image tag (latest not lastest).

Load local image into Minikube with minikube image load.

Use imagePullPolicy: IfNotPresent.

Issue: Cannot access service via http://<minikube-ip>:<nodePort>
Reason: Docker driver isolates Minikube network; your host cannot reach Minikube IP.

Solution:

Use kubectl port-forward svc/cod-guns-service 8080:80 then browse to http://localhost:8080.

Alternatively, use minikube service cod-guns-service to open URL.

Configure Minikube networking mode or use Bridged networking (advanced).

Issue: Firewall or VPN blocks connection
Solution:

Add firewall inbound rule for NodePort port (30008 TCP).

Temporarily disable VPN or configure to allow LAN traffic.

Summary
Step 3 is about deploying your Dockerized static website on Minikube Kubernetes and exposing it via a service.

Challenges often arise due to image accessibility and network isolation in Minikube’s Docker driver; these can be overcome by loading images correctly and using port-forwarding.

Once pods are running and service reachable, you can test your website in the browser successfully.
## Project Structure

