# Service
An abstract way to expose an application running on a set of Pods as a network service.

## Create service
```
kubectl apply -f nginx-service.yaml
```

## Delete service
```
kubectl delete -f nginx-service.yaml
```

## Link pods and service with `selector` labels
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app.kubernetes.io/name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
---    
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app.kubernetes.io/name: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80 
```

## Test
```
kubectl run curl --rm -ti --image krishgobinath/netutils sh
curl http://nginx-service
curl http://nginx-service.default.svc.cluster.local
```
