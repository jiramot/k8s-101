# POD
A Pods in Kubernetes abstraction that represent a group of one or more application containers, and some shared resource of those containers include:
- Share storage as Volumes
- Networking, same unique cluster IP address
- Information about how to run each container, such as the container image version or specific ports to use

## Workshop
### 1. Pod
Create pod
```
kubectl apply -f nginx-pod.yaml
```
List pod
```
kubectl get pods
```
destroy pod
```
kubectl delete pods nginx-pod
```
or
```
kubectl delete -f nginx-pod.yaml
```

#### 2. Initial container
```
kubectl apply -f init-container.yaml
kubectl get pod
```

### 3. Share network
Create
```
kubectl apply -f shared-network.yaml
```
Attach to curl container
```
kubectl attach -it shared-network -c curl
curl http://localhost
```
Destroy
```
kubectl delete -f shared-network.yaml
```

### 4. Share volume
```
kubectl apply -f shared-volumes.yaml
```
Attach to shell container
```
kubectl attach -it shared-volumes -c a
cd /data
echo "created form a container" > a.txt
```
Attach to shell2 container
```
kubectl attach -it shared-volumes -c b
cd /data
ls
cat a.txt
```
Destroy
```
kubectl destroy -f shared-volumes.yaml
```

### 4. Share Process Namespace
Create
```
kubectl apply -f shared-process-namespace.yaml
```
Attach to shell container
```
kubectl attach -it shared-process -c shell
ps
```
```
/ # ps
PID   USER     TIME  COMMAND
    1 65535     0:00 /pause
   10 root      0:00 nginx: master process nginx -g daemon off;
   41 101       0:00 nginx: worker process
   42 101       0:00 nginx: worker process
   43 101       0:00 nginx: worker process
   44 101       0:00 nginx: worker process
   45 root      0:00 sh
   54 root      0:00 ps
```
Delete
```
kubectl delete -f shared-process-namespace.yaml
```
