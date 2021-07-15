## Part1

### Q1:
	Deploy a pod named nginx-pod using the nginx:alpine image.
	Name: nginx-pod-yourname
	Image: nginx:alpine
	
### Answer1:
```Bash
kubectl run nginx-pod --image=nginx:alpine -n apx-x998-gabid
pod/nginx-pod created
```

### Q2:
	Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg.
	Pod Name: messaging
	Image: redis:alpine
	Labels: tier=msg
	
### Answer2:
```Bash
kubectl run messaging --image=redis:alpine -l tier=msg -n apx-x998-gabid
pod/messaging created
```

### Q3:
	Create a namespace named apx-x998-yourname

### Answer3:
```Bash
kubectl create ns apx-x998-gabid
namespace/apx-x998-gabid created
```

### Q4:
	Get the list of nodes in JSON format and store it in a file at /tmp/nodes-yourname

### Answer4:
```Bash
kubectl get nodes -o json > /tmp/nodes-gabid
```

### Q5:
	Create a service messaging-service to expose the messaging application within the
	cluster on port 6379.
	a. Use imperative commands - kubectl
	b. Service: messaging-service
	c. Port: 6379
	d. Type: ClusterIp
	e. Use the right labels
	
### Answer5:
```Bash
kubectl -n apx-x998-gabid expose pod messaging --name messaging-service --port 6379
```

### Q6:
	same as 5
	
### Answer6:
	same as 5





