# Kubernetes Lab

A hands-on Kubernetes lab designed to learn and practice core Kubernetes concepts, application deployment, scaling, storage, networking, security, and troubleshooting.

---

# Objectives

- Learn Kubernetes architecture and components.
- Deploy and manage applications.
- Understand Pods, ReplicaSets, Deployments, and Services.
- Configure ConfigMaps and Secrets.
- Manage persistent storage.
- Implement autoscaling.
- Deploy Ingress resources.
- Practice troubleshooting and debugging.
- Learn production best practices.

---

# Prerequisites

- Basic Linux knowledge
- Docker installed
- kubectl installed
- Kubernetes Cluster (Choose one)

  - Minikube
  - KIND
  - K3s
  - Amazon EKS
  - Azure AKS
  - Google GKE

---

# Verify Installation

```bash
kubectl version --client
kubectl cluster-info
kubectl get nodes
```

Expected Output:

```text
NAME                 STATUS   ROLES           AGE
control-plane        Ready    control-plane   XXm
```

---

# Repository Structure

```
kubernetes-lab/
│
├── 01-Namespace/
├── 02-Pods/
├── 03-ReplicaSet/
├── 04-Deployment/
├── 05-Service/
├── 06-ConfigMap/
├── 07-Secrets/
├── 08-Volumes/
├── 09-PersistentVolume/
├── 10-StatefulSet/
├── 11-DaemonSet/
├── 12-Jobs/
├── 13-CronJobs/
├── 14-Ingress/
├── 15-HPA/
├── 16-RBAC/
├── 17-NetworkPolicy/
├── 18-Helm/
├── 19-Monitoring/
├── 20-Troubleshooting/
└── README.md
```

---

# Lab 1 — Namespaces

Create namespace

```bash
kubectl create namespace dev
```

View namespaces

```bash
kubectl get ns
```

Delete namespace

```bash
kubectl delete ns dev
```

---

# Lab 2 — Pods

Create Pod

```bash
kubectl apply -f pod.yaml
```

View Pods

```bash
kubectl get pods
```

Describe Pod

```bash
kubectl describe pod nginx
```

Delete Pod

```bash
kubectl delete pod nginx
```

---

# Lab 3 — ReplicaSet

Deploy ReplicaSet

```bash
kubectl apply -f replicaset.yaml
```

Check replicas

```bash
kubectl get rs
```

Scale ReplicaSet

```bash
kubectl scale rs nginx-rs --replicas=5
```

---

# Lab 4 — Deployments

Deploy application

```bash
kubectl apply -f deployment.yaml
```

View Deployment

```bash
kubectl get deployment
```

Scale Deployment

```bash
kubectl scale deployment nginx --replicas=4
```

Rolling Update

```bash
kubectl set image deployment/nginx nginx=nginx:latest
```

Rollback

```bash
kubectl rollout undo deployment nginx
```

Deployment Status

```bash
kubectl rollout status deployment nginx
```

---

# Lab 5 — Services

ClusterIP

```bash
kubectl apply -f clusterip.yaml
```

NodePort

```bash
kubectl apply -f nodeport.yaml
```

LoadBalancer

```bash
kubectl apply -f loadbalancer.yaml
```

View Services

```bash
kubectl get svc
```

---

# Lab 6 — ConfigMaps

Create ConfigMap

```bash
kubectl apply -f configmap.yaml
```

View

```bash
kubectl get configmaps
```

Describe

```bash
kubectl describe configmap app-config
```

---

# Lab 7 — Secrets

Create Secret

```bash
kubectl apply -f secret.yaml
```

View Secrets

```bash
kubectl get secrets
```

---

# Lab 8 — Persistent Volumes

Deploy

```bash
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
```

Check

```bash
kubectl get pv
kubectl get pvc
```

---

# Lab 9 — StatefulSet

Deploy

```bash
kubectl apply -f statefulset.yaml
```

Check

```bash
kubectl get statefulsets
```

---

# Lab 10 — DaemonSet

Deploy

```bash
kubectl apply -f daemonset.yaml
```

Check

```bash
kubectl get daemonsets
```

---

# Lab 11 — Jobs

Create Job

```bash
kubectl apply -f job.yaml
```

Check

```bash
kubectl get jobs
```

---

# Lab 12 — CronJobs

Deploy

```bash
kubectl apply -f cronjob.yaml
```

View

```bash
kubectl get cronjobs
```

---

# Lab 13 — Ingress

Deploy

```bash
kubectl apply -f ingress.yaml
```

View

```bash
kubectl get ingress
```

---

# Lab 14 — Horizontal Pod Autoscaler

Create HPA

```bash
kubectl autoscale deployment nginx \
--cpu-percent=60 \
--min=2 \
--max=10
```

Check

```bash
kubectl get hpa
```

---

# Lab 15 — RBAC

Apply

```bash
kubectl apply -f serviceaccount.yaml
kubectl apply -f role.yaml
kubectl apply -f rolebinding.yaml
```

Verify

```bash
kubectl auth can-i get pods --as=system:serviceaccount:default:dev-user
```

---

# Lab 16 — Network Policies

Deploy

```bash
kubectl apply -f networkpolicy.yaml
```

Check

```bash
kubectl get networkpolicy
```

---

# Lab 17 — Helm

Install Chart

```bash
helm install nginx bitnami/nginx
```

List

```bash
helm list
```

Upgrade

```bash
helm upgrade nginx bitnami/nginx
```

Uninstall

```bash
helm uninstall nginx
```

---

# Lab 18 — Monitoring

Deploy

- Prometheus
- Grafana
- Node Exporter

Useful Commands

```bash
kubectl get pods -n monitoring
kubectl get svc -n monitoring
```

---

# Lab 19 — Troubleshooting

View Logs

```bash
kubectl logs <pod-name>
```

Describe Resources

```bash
kubectl describe pod <pod-name>
```

Execute Inside Pod

```bash
kubectl exec -it <pod-name> -- /bin/bash
```

Events

```bash
kubectl get events
```

Resource Usage

```bash
kubectl top pods
kubectl top nodes
```

---

# Common kubectl Commands

```bash
kubectl get all
kubectl get pods
kubectl get svc
kubectl get nodes
kubectl get deployments
kubectl get ingress
kubectl get pvc
kubectl get pv
kubectl get events
kubectl describe pod <pod>
kubectl logs <pod>
kubectl delete pod <pod>
kubectl apply -f file.yaml
kubectl delete -f file.yaml
kubectl edit deployment nginx
kubectl rollout history deployment nginx
kubectl rollout undo deployment nginx
```

---

# Kubernetes Architecture

```
                Kubernetes Cluster
                        │
        ┌───────────────┴───────────────┐
        │                               │
  Control Plane                   Worker Nodes
        │                               │
        ├── API Server                  ├── kubelet
        ├── Scheduler                   ├── kube-proxy
        ├── Controller Manager          ├── Container Runtime
        └── etcd                        └── Pods
```

---

# Best Practices

- Use Namespaces for environment isolation.
- Always define resource requests and limits.
- Use ConfigMaps for configuration.
- Store sensitive data in Secrets.
- Use Deployments instead of standalone Pods.
- Enable readiness and liveness probes.
- Implement RBAC with least privilege.
- Use Persistent Volumes for stateful applications.
- Monitor applications using Prometheus and Grafana.
- Regularly back up etcd.

---

# Learning Outcomes

After completing this lab, you will be able to:

- Deploy applications on Kubernetes.
- Scale applications efficiently.
- Manage storage resources.
- Configure networking.
- Secure workloads with RBAC.
- Implement autoscaling.
- Deploy stateful applications.
- Troubleshoot Kubernetes issues.
- Monitor clusters using Prometheus and Grafana.
- Understand production-grade Kubernetes practices.

---

# References

- Kubernetes Official Documentation: https://kubernetes.io/docs/
- kubectl Cheat Sheet: https://kubernetes.io/docs/reference/kubectl/cheatsheet/
- Helm Documentation: https://helm.sh/docs/

---

## Author

**Anurag Sharma**

DevOps | Cloud | Kubernetes | AWS | SRE
