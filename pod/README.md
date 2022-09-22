# POD

## Create nginx pod
```
kubectl apply -f nginx-pod.yaml
```

## List pod 
```
kubectl get pods
```

## Destroy nginx pod
```
kubectl delete pods nginx
```
or
```
kubectl delete -f nginx-pod.yaml
