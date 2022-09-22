# ConfigMap
A ConfigMap is an API object used to store non-confidential data in key-value pairs
## Pods can consume ConfigMaps as 
- environment variables
- command-line arguments
- configuration files in a volume.

## ConfigMap example
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: game-demo-configmap
data:
  # property-like keys; each key maps to a simple value
  player_initial_lives: "3"
  ui_properties_file_name: "user-interface.properties"

  # file-like keys
  game.properties: |
    enemy.types=aliens,monsters
    player.maximum-lives=5    
  user-interface.properties: |
    color.good=purple
    color.bad=yellow
    allow.textmode=true
```
### Mount configmap as environment variable
```
apiVersion: v1
kind: Pod
metadata:
  name: configmap-as-env-demo-pod
spec:
  containers:
    - name: demo
      image: alpine
      command: ["sleep", "3600"]
      env:
        # Define the environment variable
        - name: PLAYER_INITIAL_LIVES # Notice that the case is different here
                                     # from the key name in the ConfigMap.
          valueFrom:
            configMapKeyRef:
              name: game-demo-configmap # The ConfigMap this value comes from.
              key: player_initial_lives # The key to fetch.
        - name: UI_PROPERTIES_FILE_NAME
          valueFrom:
            configMapKeyRef:
              name: game-demo-configmap
              key: ui_properties_file_name
```
### Test Mount as env
```
kubectl apply -f configmap-as-env.yaml
```
```
kubectl exec --stdin --tty configmap-as-env-demo-pod -- sh
env
```

### Mount as Files in volumes
```
apiVersion: v1
kind: Pod
metadata:
  name: configmap-as-file-demo-pod
spec:
  containers:
    - name: demo
      image: alpine
      command: ["sleep", "3600"]
      volumeMounts:
      - name: config
        mountPath: "/config"
        readOnly: true
  volumes:
    # You set volumes at the Pod level, then mount them into containers inside that Pod
    - name: config
      configMap:
        # Provide the name of the ConfigMap you want to mount.
        name: game-demo
        # An array of keys from the ConfigMap to create as files
        items:
        - key: "game.properties"
          path: "game.properties"
        - key: "user-interface.properties"
          path: "user-interface.properties"
```
### Test Mount as env
```
kubectl apply -f configmap-as-files.yaml
```
```
kubectl exec --stdin --tty configmap-as-file-demo-pod -- sh
cd config
ls
cat game.properties
```
