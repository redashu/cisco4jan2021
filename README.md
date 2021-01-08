# FInal day

## kubernetes revision 

<img src="k8srecap.png">


## type of storage 

<img src="st.png">

## volume explain 

<img src="volume.png">

# EmptyDir Volume Example 

## pod creation 

```
❯ kubectl run  ashuemppod  --image=alpine  --command ping fb.com  --namespace ashu-space --dry-run=client -o yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: ashuemppod
  name: ashuemppod
  namespace: ashu-space
spec:
  containers:
  - command:
    - ping
    - fb.com
    image: alpine
    name: ashuemppod
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
❯ kubectl run  ashuemppod  --image=alpine  --command ping fb.com  --namespace ashu-space --dry-run=client -o yaml >emppod.yml


```

## POD with Volume 

```

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: ashuemppod
  name: ashuemppod
  namespace: ashu-space
spec:
  volumes:
  - name: ashuvol1 # name of volume that will be created 
    emptyDir: {}  # will take storage from random location from that minion node where it will be scheduled
  containers:
  - command:
    - ping
    - fb.com
    image: alpine
    name: ashuemppod
    volumeMounts:
    - name: ashuvol1 # same volume as above we created 
      mountPath: /mnt/cisco #this directory will be created on the POD 
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  
  ```
  
 ## Empty access
 
 ```
  kubectl  get  po -n ashu-space
NAME         READY   STATUS    RESTARTS   AGE
ashuemppod   1/1     Running   0          92s
❯ 
❯ kubectl exec -it  ashuemppod  -n ashu-space  -- sh
/ # 
/ # cd  /mnt/
/mnt # ls
cisco
/mnt # cd  cisco/
/mnt/cisco # s
sh: s: not found
/mnt/cisco # ls

```


## changing script 

```
❯ kubectl replace -f emppod.yml --force
pod "ashuemppod" deleted
pod/ashuemppod replaced
❯ kubectl  get  po -n ashu-space
NAME         READY   STATUS    RESTARTS   AGE
ashuemppod   1/1     Running   0          12s
❯ kubectl exec -it  ashuemppod  -n ashu-space  -- sh
/ # cd /mnt/cisco/
/mnt/cisco # ls
time.txt
/mnt/cisco # cat  time.txt 
Fri Jan  8 04:42:44 UTC 2021
Fri Jan  8 04:42:47 UTC 2021
Fri Jan  8 04:42:50 UTC 2021
Fri Jan  8 04:42:53 UTC 2021
Fri Jan  8 04:42:56 UTC 2021

```

## Multi container POd 

```
❯ cat  emppod.yml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: ashuemppod
    x: helloashu
  name: ashuemppod
  namespace: ashu-space
spec:
  nodeName: worker1  # static scheduling 
  volumes:
  - name: ashuvol1 # name of volume that will be created 
    emptyDir: {}  # will take storage from random location from that minion node where it will be scheduled
  containers:
  - command: ["/bin/sh","-c","while true;do date >>/mnt/cisco/index.html; sleep 3 ; done"]
    image: alpine
    name: ashuemppod
    volumeMounts:
    - name: ashuvol1 # same volume as above we created 
      mountPath: /mnt/cisco #this directory will be created on the POD automatically if not present 

  - image: nginx
    name: ashungc1 
    ports:
    - containerPort: 80
    volumeMounts: 
    - name: ashuvol1 
      mountPath: /usr/share/nginx/html  
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  
  ```
  
  ## multi container images pod
  
  <img src="multicont.png">
  
  ```
  
  ❯ cat  emppod.yml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: ashuemppod
    x: helloashu
  name: ashuemppod
  namespace: ashu-space
spec:
  nodeName: worker1  # static scheduling 
  volumes:
  - name: ashuvol1 # name of volume that will be created 
    emptyDir: {}  # will take storage from random location from that minion node where it will be scheduled
  containers:
  - command: ["/bin/sh","-c","while true;do date >>/mnt/cisco/index.html; sleep 3 ; done"]
    image: alpine
    name: ashuemppod
    volumeMounts:
    - name: ashuvol1 # same volume as above we created 
      mountPath: /mnt/cisco #this directory will be created on the POD automatically if not present 

  - image: nginx
    name: ashungc1 
    ports:
    - containerPort: 80
    volumeMounts: 
    - name: ashuvol1 
      mountPath: /usr/share/nginx/html  
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
❯ kubectl replace -f  emppod.yml --force
pod "ashuemppod" deleted
pod/ashuemppod replaced

```

# HostPath volume 

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: hostpod
  name: hostpod
spec:
  volumes:
  - name: ashuvol2
    hostPath:
     path: /data123  # location from Minion Node
     type: DirectoryOrCreate  # check if not present on the host then create it 
  - name: ashuvol3
    emptyDir: {} 
  containers:
  - image: alpine
    name: hostpod
    command: ["/bin/sh","-c","while true;do cal >>/mnt/data.txt;sleep 5 ;done"]
    volumeMounts:
    - name: ashuvol2
      mountPath: /mnt/
    - name: ashuvol3
      mountPath: /datanew  
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  
  ```
  
  # portainer with Deployment 
  
  ```
  ❯ cat portainer.yml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: portainer
  name: portainer
spec:
  replicas: 1
  selector:
    matchLabels:
      app: portainer
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: portainer
    spec:
      volumes:
      - name: ashuweb
        hostPath:
         path: /var/run/docker.sock
         type: Socket
      containers:
      - image: portainer/portainer
        name: portainer
        ports:
        - containerPort: 9000
        volumeMounts:
        - name: ashuweb
          mountPath: /var/run/docker.sock
        resources: {}
        
  ```
  
  # LoadBalancer service 
  
  <img src="lbsvc.png">
  
  # Persistent volume (PV)
  
  <img src="pv.png">
  
  ## PV 
  
  ```
  ❯ cat ashupv.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: ashu-pv-1
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteMany   # ReadWriteOnce , ReadOnlyMany , ReadWriteMany 
  nfs:
    server: 172.31.25.191  # IP of NFS server 
    path: /storage/ashu  # location of NFS server 
    
```

## PVC

```

❯ cat ashu-pvc.yml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: ashu-pvc
  namespace: ashu-space 
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: ""
  resources:
    requests:
      storage: 2Gi
      
```

## pvc bound 

```
❯ kubectl apply -f ashu-pvc.yml
persistentvolumeclaim/ashu-pvc created
❯ kubectl get pvc -n ashu-space
NAME       STATUS   VOLUME        CAPACITY   ACCESS MODES   STORAGECLASS   AGE
ashu-pvc   Bound    saurav-pv-1   2Gi        RWX                           7s
❯ kubectl get pv
NAME          CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM                 STORAGECLASS   REASON   AGE
ashu-pv-1     5Gi        RWX            Retain           Available                                                 4m26s
ragpv1        2Gi        RWX            Retain           Available                                                 6m22s
saurav-pv-1   2Gi        RWX            Retain           Bound       ashu-space/ashu-pvc

```

# Users in k8s

<img src="user.png">

```
❯ kubectl  get  serviceaccount -n ashu-space
NAME      SECRETS   AGE
default   1         24h
❯ kubectl  get  sa  -n ashu-space
NAME      SECRETS   AGE
default   1         24h

```



