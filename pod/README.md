# POD
A Pods in Kubernetes abstraction that represent a group of one or more application containers, and some shared resource of those containers include:
- Share storage as Volumes
- Networking, same unique cluster IP address
- Information about how to run each container, such as the container image version or specific ports to use

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
