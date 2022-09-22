# Deployment
A deployment provides declarative updates for Pods and ReplicaSets

## Create nginx deployment
```
kubectl apply -f nginx-deployment.yaml
```
## List deployments
```
kubectl get deployments
```
## Get deployment details
```
kubectl describe deployment ${deployment-name}
```
## List replica set
```
kubectl get rs
```
## Get replica set details
```
kubectl describe rs ${replica-set-name}
```
## Delete deployment
```
kubectl delete deployment nginx-deployment
```
or
```
kubectl delete -f nginx-deployment.yaml
```