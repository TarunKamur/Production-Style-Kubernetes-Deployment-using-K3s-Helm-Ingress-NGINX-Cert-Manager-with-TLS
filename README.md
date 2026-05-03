# 🚀 End-to-End Kubernetes Deployment on K3s (Production-Style)

## 📌 Overview

This project demonstrates a **complete end-to-end Kubernetes deployment** using:

* **K3s** (Lightweight Kubernetes Cluster)
* **Helm** (Package Management)
* **Ingress NGINX** (Traffic Routing)
* **Cert-Manager** (Automated TLS/SSL with Let’s Encrypt)
* **Custom Application Deployment**

It includes:

---
* Full setup from scratch

* Real-time troubleshooting
DevOps & Cloud Engineer
* Common production bottlenecks

B Tarun Kumar
---

# 🧱 Architecture


# 👨‍💻 Author
```
User → DNS → Public IP → Ingress NGINX → Service → Pod → Application
---

                         ↓

                    Cert-Manager → Let’s Encrypt (TLS)
* Blue/Green deployment
```
* Multi-service Helm charts

* Monitoring (Prometheus + Grafana)
---

# ⚙️ 1. K3s Cluster Setup

* CI/CD (GitHub Actions)

# 🚀 Future Enhancements

## Install K3s


---
```bash
curl -sfL https://get.k3s.io | sh -s - --disable traefik
```

## Verify Cluster

* Debugging requires layer-by-layer approach
```bash
kubectl get nodes


* Ingress controls external traffic
```
* Cert-Manager automates TLS lifecycle

## Configure kubeconfig
# 🎯 Key Learnings

* Helm simplifies Kubernetes deployments

```bash
---

export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```

---
```

```
DNS → Network → Ingress → Service → Pod → App

# 📦 2. Install Helm

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
helm version
```


# 🔥 DevOps Debug Strategy
---

# 🌐 3. Install Ingress NGINX (Helm)
---


```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
| TLS     | Staging cert      |
| App     | Wrong port        |

helm repo update

helm install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace \
  --set controller.service.type=LoadBalancer
Or 

helm install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx --create-namespace \
  --set controller.hostNetwork=true \
  --set controller.service.type=ClusterIP
```

| Service | Selector mismatch |
## Verify

```bash
kubectl get pods -n ingress-nginx
```
| Ingress | Wrong class       |

---

| Network | Ports blocked     |
# 🔐 4. Install Cert-Manager (Helm)

```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/latest/download/cert-manager.crds.yaml

helm repo add jetstack https://charts.jetstack.io
helm repo update

helm install cert-manager jetstack/cert-manager \
  --namespace cert-manager --create-namespace \
  --set installCRDs=true
  
```
| ------- | ----------------- |

## Verify

```bash
kubectl get pods -n cert-manager


# ⚠️ Common Bottlenecks (Real Production)

| Layer   | Problem           |
---
```

---

* Verify correct certificate served
# 📜 5. Configure ClusterIssuer
* Clear browser cache

* Ensure production issuer
```yaml

✔ Fix:
apiVersion: cert-manager.io/v1

kind: ClusterIssuer
metadata:
  name: letsencrypt-prod
spec:

## ❌ Issue 7: TLS Error (ERR_CERT_AUTHORITY_INVALID)
  acme:
---
    email: your-email@gmail.com

    server: https://acme-v02.api.letsencrypt.org/directory
    privateKeySecretRef:
      name: letsencrypt-prod
    solvers:
    - http01:
```
        ingress:
          class: nginx
```
sudo ufw allow 80
sudo ufw allow 443

```bash
kubectl apply -f cluster-issuer.yaml
```

---

# 🚀 6. Deploy Application using Helm

```bash

```bash
helm create demo-app
cd demo-app
```

* Open ports:
## Update values.yaml

```yaml
service:
## ❌ Issue 6: Port Not Accessible

✔ Fix:

---

  port: 80

ingress:

  enabled: true
* Verify service name & port
  className: nginx
* Check ingress host
  hosts:
    - host: demo.yourdomain.com
      paths:
        - path: /

          pathType: Prefix
✔ Fix:
  tls:
    - secretName: demo-app-tls
      hosts:
        - demo.yourdomain.com
```

---

## Update ingress.yaml


```yaml
annotations:
  cert-manager.io/cluster-issuer: letsencrypt-prod
```

---

## ❌ Issue 5: 404 from NGINX
## Deploy

```bash
helm upgrade --install demo-app .
```

---

# 🌍 7. DNS Configuration


Point domain to VM public IP:
---

```
A Record:
demo.yourdomain.com → <PUBLIC_IP>
```

---


# 🔍 8. Verification

```bash
kubectl get ingress
kubectl get cert
kubectl get pods
```


* Match labels between Service and Pod
Access:

```
https://demo.yourdomain.com
```
kubectl get endpoints
✔ Fix:
```

```bash


## ❌ Issue 4: Service Has No Endpoints

---


---
# 🛠️ Real-Time Troubleshooting Guide

---
```

kubectl rollout restart deployment ingress-nginx-controller -n ingress-nginx
## ❌ Issue 1: Domain Not Resolving

```bash

```bash
nslookup demo.yourdomain.com
```

✔ Fix:

* Restart ingress controller
* Check DNS A record

* Ensure correct nameservers
✔ Fix:


---
```

## ❌ Issue 2: SSL Not Working

```bash
kubectl describe certificate
```

✔ Fix:
Using default certificate

* Use letsencrypt-prod (not staging)
* Verify ingress annotation

---
```
```


Error:

kubectl logs -n ingress-nginx <pod>
## ❌ Issue 3: Default Fake Certificate


```bash
```bash

## ❌ Issue 3: Default Fake Certificate
kubectl logs -n ingress-nginx <pod>
---
```

Error:


* Verify ingress annotation
```
Using default certificate
```


* Use letsencrypt-prod (not staging)
✔ Fix:

* Restart ingress controller

✔ Fix:

```
```bash
kubectl rollout restart deployment ingress-nginx-controller -n ingress-nginx
kubectl describe certificate

```bash
```

## ❌ Issue 2: SSL Not Working
---


## ❌ Issue 4: Service Has No Endpoints

---

```bash
kubectl get endpoints
```

✔ Fix:
* Ensure correct nameservers

* Match labels between Service and Pod

---


* Check DNS A record
## ❌ Issue 5: 404 from NGINX
nslookup demo.yourdomain.com
```

✔ Fix:

✔ Fix:
```bash

## ❌ Issue 1: Domain Not Resolving

* Check ingress host
---

* Verify service name & port


---
# 🛠️ Real-Time Troubleshooting Guide

---

## ❌ Issue 6: Port Not Accessible

https://demo.yourdomain.com
```

✔ Fix:


```
* Open ports:

```bash
sudo ufw allow 80
sudo ufw allow 443

Access:
```

---
```

kubectl get pods
## ❌ Issue 7: TLS Error (ERR_CERT_AUTHORITY_INVALID)

kubectl get cert
✔ Fix:
kubectl get ingress

* Ensure production issuer
* Clear browser cache
* Verify correct certificate served
```bash

---

# ⚠️ Common Bottlenecks (Real Production)

| Layer   | Problem           |
| ------- | ----------------- |
| DNS     | Wrong IP mapping  |

---

# 🔍 8. Verification
demo.yourdomain.com → <PUBLIC_IP>

```
| Network | Ports blocked     |
| Ingress | Wrong class       |
A Record:
| Service | Selector mismatch |
```

Point domain to VM public IP:
| TLS     | Staging cert      |

| App     | Wrong port        |
# 🌍 7. DNS Configuration


---
---

# 🔥 DevOps Debug Strategy

```

```
DNS → Network → Ingress → Service → Pod → App
```


helm upgrade --install demo-app .
```bash
## Deploy

---

---
# 🎯 Key Learnings


```
```

---

## Update ingress.yaml

annotations:
  cert-manager.io/cluster-issuer: letsencrypt-prod
```yaml
* Helm simplifies Kubernetes deployments
* Cert-Manager automates TLS lifecycle
* Ingress controls external traffic
        - demo.yourdomain.com
* Debugging requires layer-by-layer approach

      hosts:
---
  tls:
    - secretName: demo-app-tls

# 🚀 Future Enhancements
        - path: /
          pathType: Prefix

      paths:
    - host: demo.yourdomain.com
* CI/CD (GitHub Actions)
* Monitoring (Prometheus + Grafana)
# 🚀 End-to-End Kubernetes Deployment on K3s (Production-Style)
  hosts:

  className: nginx

  enabled: true
ingress:
## 📌 Overview

This project demonstrates a **complete end-to-end Kubernetes deployment** using:

* **K3s** (Lightweight Kubernetes Cluster)
  port: 80
* **Helm** (Package Management)
* **Ingress NGINX** (Traffic Routing)
* **Cert-Manager** (Automated TLS/SSL with Let’s Encrypt)
* **Custom Application Deployment**

It includes:
service:

```yaml

* Full setup from scratch
## Update values.yaml
* Real-time troubleshooting
* Common production bottlenecks

---

# 🧱 Architecture


cd demo-app
```
```
```bash
```

---
helm create demo-app

```bash
# 🚀 6. Deploy Application using Helm

kubectl apply -f cluster-issuer.yaml
User → DNS → Public IP → Ingress NGINX → Service → Pod → Application

          class: nginx
```
        ingress:
    - http01:
    solvers:
    privateKeySecretRef:
      name: letsencrypt-prod
    server: https://acme-v02.api.letsencrypt.org/directory
                         ↓
    email: your-email@gmail.com
  acme:
                    Cert-Manager → Let’s Encrypt (TLS)
spec:
  name: letsencrypt-prod
kind: ClusterIssuer
metadata:
```
apiVersion: cert-manager.io/v1
```yaml


# 📜 5. Configure ClusterIssuer
```bash
---

  --namespace cert-manager --create-namespace \

  --set installCRDs=true
```
```

```bash
kubectl get pods -n cert-manager

## Verify
helm install cert-manager jetstack/cert-manager \
helm repo update

helm repo add jetstack https://charts.jetstack.io


# 🔐 4. Install Cert-Manager (Helm)

---
kubectl get pods -n ingress-nginx
```
```bash

## Verify
---

```
  --set controller.hostNetwork=true \
  --set controller.service.type=ClusterIP
  --namespace ingress-nginx --create-namespace \

helm install ingress-nginx ingress-nginx/ingress-nginx \

helm repo update
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
```bash


# 🌐 3. Install Ingress NGINX (Helm)
---

# ⚙️ 1. K3s Cluster Setup
```

## Install K3s
helm version

curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```bash
curl -sfL https://get.k3s.io | sh -
```

```bash

## Verify Cluster

```bash
kubectl get nodes
# 📦 2. Install Helm
```


## Configure kubeconfig

```bash
---
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```

