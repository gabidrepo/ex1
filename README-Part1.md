Q1:
	Deploy a pod named nginx-pod using the nginx:alpine image.
	Name: nginx-pod-yourname
	Image: nginx:alpine
	
Answer:
	kubectl run nginx-pod --image=nginx:alpine --restart=Never
