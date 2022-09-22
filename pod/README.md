# POD
A Pods in Kubernetes abstraction that represent a group of one or more application containers, and some shared resource of those containers include:
- Share storage as Volumes
- Networking, same unique cluster IP address
- Information about how to run each container, such as the container image version or specific ports to use

## Workshop
### 1. Basic command
#### Create nginx pod
```
kubectl apply -f nginx-pod.yaml
```
#### List pod
```
kubectl get pods
```
#### Destroy nginx pod
```
kubectl delete pods nginx
```
or
```
kubectl delete -f nginx-pod.yaml
```

## Multi-container
### 2. Share network
```
kubectl apply -f shared-network.yaml
```
Attach to shell container
```
kubectl attach -it nginx -c shell
wget http://localhost
cat index.html
```

### 3. Share volume
```
kubectl apply -f shared-volumes.yaml
```
Attach to shell container
```
kubectl attach -it nginx -c shell
cd /data
echo "hello" > a.txt
```
Attach to shell2 container
```
kubectl attach -it nginx -c shell2
cd /data2
ls
cat a.txt
```
### 4. Share Process Namespace
```
kubectl apply shared-process-namespace.yaml
```
Attach to shell container
```
kubectl attach -it nginx -c shell
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
#### 5. Initial container
```
kubectl apply -f init-container.yaml
kubectl get pod
```