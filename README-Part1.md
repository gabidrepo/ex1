## Part1

### Q1:
	Deploy a pod named nginx-pod using the nginx:alpine image.
	Name: nginx-pod-yourname
	Image: nginx:alpine
	
### Answer1:
```Bash
kubectl run nginx-pod --image=nginx:alpine --restart=Never
pod/nginx-pod created
```

### Q2:
	Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg.
	Pod Name: messaging
	Image: redis:alpine
	Labels: tier=msg
	
### Answer2:
```Bash
kubectl run messaging --image=redis:alpine -l tier=msg
pod/messaging created
```

### Q3:
	Create a namespace named apx-x998-yourname

### Answer3:
```Bash
kubectl create ns apx-x998-gabid
namespace/apx-x998-gabid created
```
