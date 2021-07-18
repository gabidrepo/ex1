## Part1

### Q1:
	Deploy a pod named nginx-pod using the nginx:alpine image.
	Name: nginx-pod-yourname
	Image: nginx:alpine
	
### Answer1:
```Bash
>kubectl run nginx-pod --image=nginx:alpine -n apx-x998-gabid
pod/nginx-pod created
```

### Q2:
	Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg.
	Pod Name: messaging
	Image: redis:alpine
	Labels: tier=msg
	
### Answer2:
```Bash
>kubectl run messaging --image=redis:alpine -l tier=msg -n apx-x998-gabid
pod/messaging created
```

### Q3:
	Create a namespace named apx-x998-yourname

### Answer3:
```Bash
>kubectl create ns apx-x998-gabid
namespace/apx-x998-gabid created
```

### Q4:
	Get the list of nodes in JSON format and store it in a file at /tmp/nodes-yourname

### Answer4:
```Bash
>kubectl get nodes -o json > /tmp/nodes-gabid
```

### Q5:
	Create a service messaging-service to expose the messaging application within the
	cluster on port 6379.
	a. Use imperative commands - >kubectl
	b. Service: messaging-service
	c. Port: 6379
	d. Type: ClusterIp
	e. Use the right labels
	
### Answer5:
```Bash
>kubectl -n apx-x998-gabid expose pod messaging --name messaging-service --port 6379
service/messaging-service exposed
```

### Q6:
	same as 5
	
### Answer6:
	same as 5

### Q7:
	Create a deployment named hr-web-app using the image kodekloud/webapp-color
	with 2 replicas
	a. Name: hr-web-app
	b. Image: kodekloud/webapp-color
	c. Replicas: 2
	
### Answer7:
```Bash
>kubectl create deploy hr-web-app --image=kodekloud/webapp-color
deployment.apps/hr-web-app created

>kubectl scale deploy hr-web-app --replicas=2
deployment.apps/hr-web-app scaled

```

### Q8:
	Create a static pod named static-busybox on the master node that uses the busybox
	image and the command sleep 1000
	a. Name: static-busybox
	b. Image: busybox

### Answer8:
[busybox.yaml](/busybox.yaml)
```yaml
>kubectl create -f busybox.yaml
pod/static-busybox created

apiVersion: v1
kind: Pod
metadata:
  name: static-busybox
spec:
  containers:
   - name: static-busybox
     image: busybox
     command: ["sleep"]
     args: ["1000"]
```

### Q9:
	Create a POD in the finance-yourname namespace named temp-bus with the image
	redis:alpine
	a. Name: temp-bus
	b. Image Name: redis:alpine

### Answer9:
```yaml
>kubectl create ns finance-gabid
namespace/finance-gabid created

>kubectl run temp-bus -n finance-gabid --image=redis:alpine
pod/temp-bus created
```
### Q10:
	Create a Persistent Volume with the given specification
	a. Volume Name: pv-analytics
	b. Storage: 100Mi
	c. Access modes: ReadWriteMany
	d. Host Path: /pv/data-analytics
### Answer10:
[persistance-vol.yaml](/persistance-vol.yaml)
```yaml
>kubectl create -f persistance-vol.yaml

apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-analytics
spec:
 volumes:
  - name: pv-analytics
    hostPath:
      path: /pv/data-analytics
  capacity:    
    storage: 100Mi  
  accessModes:    
  - ReadWriteMany
```

### Q11:
	Create a Pod called redis-storage-yourname with image: redis:alpine with a Volume
	of type emptyDir that lasts for the life of the Pod. specs:.
	a. Pod named 'redis-storage-yourname'
	b. Pod 'redis-storage-yourname' uses Volume type of emptyDir
	c. Pod 'redis-storage-yourname' uses volumeMount with mountPath =/data/redis
	
### Answer11:
[redis-storage-gabid.yaml](/redis-storage-gabid.yaml)
```yaml
>kubectl create -f redis-storage-gabid.yaml
pod/redis-stroage-gabid created

apiVersion: v1
kind: Pod
metadata:
  name: redis-stroage-gabid
spec:
  containers:
  - image: redis:alpine
    name: redis-storage-gabid
    volumeMounts:
    - mountPath: /data/redis
      name: redis-storage-gabid
  volumes:
  - name: redis-storage-gabid
    emptyDir: {}
```
### Q12:
	Create this pod and attached it a persistent volume called pv-1
	a. Make sure the PV mountPath is hostbase : /data
	apiVersion: v1
	kind: Pod
	metadata:
	creationTimestamp: null
	labels:
	run: use-pv
	name: use-pvspec-yourname
	containers:
	- image: nginx
	name: use-pv
	resources: {}
	dnsPolicy: ClusterFirst
	restartPolicy: Always
	status: {}
	
### Answer12:
[pv-volume.yaml](/pv-volume.yaml)

[pv-claim.yaml](/pv-claim.yaml)

[pv-pod.yaml](/pv-pod.yaml)

```bash
>kubectl apply -f pv-volume.yaml
persistentvolume/pv1 created

>kubectl get pv pv1
NAME   CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE
pv1    100Mi      RWX            Retain           Available                                   41s

kubectl apply -f pv-claim.yaml
persistentvolumeclaim/pv1-claim created

>kubectl apply -f pv-pod.yaml
pod/use-pv-gabid created

>kubectl get pods
NAME                            READY   STATUS      RESTARTS   AGE
static-busybox                  1/1     Running     17         5h47m
use-pv-gabid                    1/1     Running     0          63s
```


********************
### Q13:
	Create a new deployment called nginx-deploy, with image nginx:1.16 and 1 replica.
	Record the version. Next upgrade the deployment to version 1.17 using rolling
	update. Make sure that the version upgrade is recorded in the resource annotation.
	a. Deployment : nginx-deploy. Image: nginx:1.16
	b. Image: nginx:1.16
	c. Task: Upgrade the version of the deployment to 1:17
	d. Task: Record the changes for the image upgrade
### Answer13:
```yaml
>kubectl create deploy nginx-deploy --image=nginx:1.16 --replicas=1
pod/nginx-deploy created

>kubectl rollout history deploy nginx-deploy
deployment.apps/nginx-deploy
REVISION  CHANGE-CAUSE
1         <none>

>kubectl set image deployment/nginx-deploy nginx-deploy=nginx:1.17 --record
deployment.apps/nginx-deploy image updated

```

### Q14:
	Create an nginx pod called nginx-resolver using image nginx, expose it internally
	with a service called nginx-resolver-service. Test that you are able to look up the8363
	service and pod names from within the cluster. Use the image: busybox:1.28 for dns
	lookup. Record results in /root/nginx-yourname.svc and /root/nginx-yourname.pod

### Answer14:
```yaml
>kubectl run nginx-resolver --image=nginx --port=80
pod/nginx-resolver created

>kubectl expose pod nginx-resolver --name=nginx-resolver-service --port=80 --target-port=80 --type=ClusterIP
service/nginx-resolver-service exposed

>kubectl run test-nslookup --image=busybox:1.28 --rm -it -- nslookup nginx-resolver-service > /root/nginx-gabid.svc

>kubectl run test-nslookup --image=busybox:1.28 --rm -it -- nslookup nginx-resolver.pod > /root/nginx-gabid.pod
```

### Q15:
Create a static pod on node01 called nginx-critical with image nginx. Create this pod
on node01 and make sure that it is recreated/restarted automatically in case of a
failure.

### Answer15:

[nginx-critical.yaml](/nginx-critical.yaml)
```yaml
>kubectl create -f nginx-critical.yaml
pod/nginx-critical created

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx-critical
  name: nginx-critical
spec:
  containers:
  - image: nginx
    name: nginx-critical
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

### Q16:
	Create a pod called multi-pod with two containers.
	Container 1, name: alpha, image: nginx
	Container 2: beta, image: busybox, command sleep 4800.
	a. Environment Variables:
	i. container 1:
	ii. name: alpha
	iii. Container 2:
	iv. name: beta
	
### Answer16:
 
[multi-pod.yaml](/multi-pod.yaml)
```yaml
>kubectl create -f multi-pod.yaml
pod/multi-pod created

apiVersion: v1
kind: Pod
metadata:
  name: multi-pod
spec:
  containers:
  - image: nginx
    imagePullPolicy: IfNotPresent
    name: alpha
    env:
    - name: name
      value: alpha
  - image: busybox
    name: beta
    env:
    - name: name
      value: beta
    command: ["sleep","4800"]
```
