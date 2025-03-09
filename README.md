# MLOps Kubernetes Project

Ce projet implémente une architecture **MLOps** avec **Kubernetes** pour le déploiement d'un modèle de Machine Learning sur l'**Iris Dataset**. Il comprend :
- Un **backend** (API ML) servant des prédictions, déployé sous forme de **3 réplicas**.
- Un **frontend** interagissant avec l'API.
- Une connexion entre le frontend et l'API via un **service Kubernetes**.
- Les images frontend et backend sont accessibles [ici](https://github.com/marinaKpamegan/mlops): 

---

## 🚀 Installation et Déploiement

### 1️⃣ Prérequis
Avant de commencer, assurez-vous d'avoir :
- [Docker](https://www.docker.com/get-started)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

### 2️⃣ Lancer Kubernetes
Démarrez votre cluster Kubernetes local avec Docker Desktop ou Minikube.

### 3️⃣ Construire les images Docker
Ajoutez les images Docker :
```bash
# Construire les images à partir du repo Mlops en trois versions (dans le endpoint /version de l'application)
docker build -t mlops-server:0.1.0 .
docker build -t mlops-server:0.2.0 .
docker build -t mlops-server:0.3.0 .
docker build -t mlops-client:latest .
```

### 4️⃣ Déployer le backend (API ML) et frontend
```bash
kubectl apply -f deployment.yaml
```
Vérifiez les pods :
```bash
kubectl get pods
```

### 5️⃣ Vérifier les services

```bash
kubectl get services
```

## 🔄 Tester la Communication
Testez manuellement l'API du backend :
```bash
kubectl port-forward service/mlops-api-service 8000:8000
curl http://localhost:8000/version
```
Vous devriez voir : `{"version": "0.1.0"}` et parfois `{"version": "0.2.0"}` due au déploiement canary

---

## 📌 Nettoyage
Si vous souhaitez supprimer les ressources Kubernetes :
```bash
kubectl delete deployment mlops-server mlops-client
kubectl delete service mlops-api-service mlops-client-service
```





