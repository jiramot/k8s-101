# Secret
A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key
Such information might otherwise be put in a Pod specification or in a container image but you don't need to include in your application code

## !! Unencrypted by default, 
## Use case
- As file in volume
- As container environment
- pull image form registry by kubelet

## Create secret
```
kubectl apply -f secret.yaml
```
## List secret
```
kubectl get secret
```
## Get secret detail
```
kubectl describe secret demo-secret
```
```
Name:         demo-secret
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
PASSWORD:   12 bytes
USER_NAME:  5 bytes
```
## Decode secret
```
kubectl get secret demo-secret -o jsonpath='{.data}'
```
```
{"PASSWORD":"MWYyZDFlMmU2N2Rm","USER_NAME":"YWRtaW4="}
```
```
kubectl get secret demo-secret -o jsonpath='{.data.PASSWORD}' | base64 --decode
```

## Demo secret as env
```
kubectl apply -f secret-as-env.yaml
kubectl get pods
kubectl exec --stdin --tty secret-as-env-demo-pod -- sh

env
```
