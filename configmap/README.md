# ConfigMap
A ConfigMap is an API object used to store non-confidential data in key-value pairs
## Pods can consume ConfigMaps as 
- environment variables
- command-line arguments
- configuration files in a volume.

### 1. Configmap as Env
Create
```
kubectl apply -f configmap-as-env.yaml
```
Print configmap as yml
```
kubectl get configmap demo-configmap -o yaml
```
Show pod with sector label app=configmap-env
```
kubectl get pod --selector=app=configmap-env
```
Attach to pod
```
kubectl exec --stdin --tty ${POD_NAME} -- sh
env
```

### 2. Configmap as File volumes
Create
```
kubectl apply -f configmap-as-env.yaml
```
Show pod with sector label app=configmap-volumes
```
kubectl get pod --selector=app=configmap-volumes
```
Attach to pod
```
kubectl exec --stdin --tty ${POD_NAME} -- sh
cd config
ls
cat game.properties
```
