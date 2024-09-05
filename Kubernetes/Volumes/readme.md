
## K8s Volume types:
1. EmptyDir
2. HostPath
3. PersistentVolume
4. PersistanceVolumeClaim

1. EmptyDir
   
```yaml
apiVersion: v1
kind: Pod
metadata: 
 name: pod-1

spec:
  containers:
    - name: cont1
      image: nginx
      volumeMounts:
      - name: ebs
        mountPath: /tmp/data

  volumes: 
  - name: ebs
    emptyDir:
      sizeLimit: 500Mi
```
````
apiVersion: v1
kind: Pod
metadata:
  name: emptydir-pod
spec:
  containers:
  - name: my-container
    image: nginx
    volumeMounts:
    - mountPath: /usr/share/nginx/html
      name: my-emptydir
  volumes:
  - name: my-emptydir
    emptyDir: {}
````
````
apiVersion: v1
kind: Pod
metadata:
  name: hostpath-pod
spec:
  containers:
  - name: my-container
    image: nginx
    volumeMounts:
    - mountPath: /usr/share/nginx/html
      name: my-hostpath
  volumes:
  - name: my-hostpath
    hostPath:
      path: /data/nginx
      type: DirectoryOrCreate
````
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-example
spec:
  capacity:
    storage: 5Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: manual
  hostPath:
    path: "/mnt/data"
```
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-example
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
  storageClassName: manual
```
**Attach PV to pod**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: pv-example
  volumes:
    - name: pv-example
      persistentVolumeClaim:
        claimName: pvc-example
```
