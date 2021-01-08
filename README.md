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



