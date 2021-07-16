## Part2

### Q1:
 Type the command for:
Get pods with label information
### Answer1:
```Bash
>kubectl run nginx-pod --image=nginx:alpine -n apx-x998-gabid
pod/nginx-pod created
```

### Q2:
Create 5 nginx pods in which two of them is labeled env=prod and three of them is
labeled env=dev
### Q3:
Verify all the pods are created with correct labels
### Q4:
Get the pods with label env=dev
### Q5:
Get the pods with label env=dev and also output the labels8363
### Q6:
Get the pods with label env=prod
### Q7:
Get the pods with label env=prod and also output the labels
### Q8:
Get the pods with label env
### Q9:
Get the pods with labels env=dev and env=prod
### Q10:
Get the pods with labels env=dev and env=prod and output the labels as well
### Q11:
Change the label for one of the pod to env=uat and list all the pods to verify
### Q12:
Remove the labels for the pods that we created now and verify all the labels are removed
### Q13:
Let’s add the label app=nginx for all the pods and verify (using kubectl)
### Q14:
Get all the nodes with labels (if using minikube you would get only master node)
### Q15:
Label the worker node nodeName=nginxnode
### Q16:
```yaml
Create a Pod that will be deployed on the worker node with the label
nodeName=nginxnode
Add the nodeSelector to the below and create the pod
apiVersion: v1
kind: Pod
metadata:
creationTimestamp: null
labels:
run: nginx
name: nginx
spec:
containers:
- image: nginx
name: nginx8363
resources: {}
dnsPolicy: ClusterFirst
restartPolicy: Never
status: {}
```
### Q17:
Verify the pod that it is scheduled with the node selector on the right node… fix it if
it’s not behind scheduled.
### Q18:
Verify the pod nginx that we just created has this label
