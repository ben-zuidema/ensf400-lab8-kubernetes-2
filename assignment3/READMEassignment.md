# ENSF 400 - Assignment 3 - Kubernetes - Ben Zuidema

## Setup 
1. Start MiniKube
```bash
minikube start
```

2. Enable Ingress
```bash
minikube addons enable ingress
```

3. Set uo minikube docker environment
```bash
eval $(minikube docker-env)
```

4. Pull images
```bash
docker pull ghcr.io/denoslab/ensf400-sample-app:v1
docker pull ghcr.io/denoslab/ensf400-sample-app:v2
```

## Deployment
Deploy Nginx, backend apps, and Ingresses

1. Deploy Nginx
```bash
kubectl apply -f nginx-dep.yaml
kubectl apply -f nginx-configmap.yaml
kubectl apply -f nginx-svc.yaml
```

2. Deploy backend apps
```bash
kubectl apply -f app-1-dep.yaml
kubectl apply -f app-1-svc.yaml
kubectl apply -f app-2-dep.yaml
kubectl apply -f app-2-svc.yaml
```

3. Deploy Ingresses
```bash
kubectl apply -f nginx-ingress.yaml
kubectl apply -f app-1-ingress.yaml
kubectl apply -f app-2-ingress.yaml
```

## Verification

Verify Nginx
```bash
curl http://$(minikube ip)
```

Expected output:
```
Hello World from [app-1-dep-<Some-Characters>]
Hello World from [app-2-dep-<Some-Characters>]
```

## Clean Up
1. Delete all deployments
```bash
kubectl delete -f nginx-dep.yaml
kubectl delete -f nginx-configmap.yaml
kubectl delete -f nginx-svc.yaml
kubectl delete -f app-1-dep.yaml
kubectl delete -f app-1-svc.yaml
kubectl delete -f app-2-dep.yaml
kubectl delete -f app-2-svc.yaml
kubectl delete -f nginx-ingress.yaml
kubectl delete -f app-1-ingress.yaml
kubectl delete -f app-2-ingress.yaml
```

2. Stop MiniKube
```bash
minikube stop
```

