# Ping Pong API

## Endpoints
- /ping - Responds with {'pong'}
- /pong - Responds with {'ping'}
- /professional-ping-pong - Responds with {'pong'} 90% of the time
- /amateur-ping-pong - Responds with {'pong'} 70% of the time
- /chance-ping-pong - Responds with {'ping'} 50% of the time and {'pong'} 50% of the time

## Description
This is a simple API to test that the RapidAPI/Mashape API Proxy is working. When you access /ping, the API will return a JSON that contains "pong"

## Usage
If you want to run this project locally - please install the following:
 
- [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/)
- [Docker](https://www.docker.com/get-started/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/)

### Clone the repository
```git clone https://github.com/Leon-Africa/ping-pong-devops.git```

### Start Kubernetes Cluster
```./kubernetes/kind/local/kind-with-registry.sh```

### Cluster Config
```kubectl cluster-info --context kind-kind```

### List Container
```docker ps```

You will see the kubernetes node and the local docker registry

### Build the image
```docker compose build```

### Push to local docker registry 
```docker compose push```

### Check local repository
```curl -X GET http://127.0.0.1:5001/v2/_catalog```

### Setup Nginx Ingress
```kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml```

### Wait to process requests
```kubectl wait --namespace ingress-nginx \
--for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s
  ```
  
### Deploy the application
```kubectl apply -f kubernetes/kind/deployment.yml```

### Confirm Pod creation
```kubectl get pods```

### Interact with [Endpoints](https://github.com/Leon-Africa/ping-pong-devops.git#endpoints) [When Pods are READY]
- ```curl localhost/biconomy/ping ```
- ```curl localhost/biconomy-2/pong``` 
