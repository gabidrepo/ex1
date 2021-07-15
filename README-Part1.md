## Part1

### Q1:
	Deploy a pod named nginx-pod using the nginx:alpine image.
	Name: nginx-pod-yourname
	Image: nginx:alpine
	
### Answer:
```Bash
kubectl run nginx-pod --image=nginx:alpine --restart=Never
```
