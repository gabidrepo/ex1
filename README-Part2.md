## Part2

### Q1:
 Type the command for:
Get pods with label information
### Answer1:
```yaml
>kubectl get pods --show-labels
```

### Q2:
Create 5 nginx pods in which two of them is labeled env=prod and three of them is
labeled env=dev
### Answer2:
```yaml
>kubectl run ndev1 --image=nginx --labels=env=dev
>kubectl run ndev2 --image=nginx --labels=env=dev
>kubectl run ndev3 --image=nginx --labels=env=dev
>kubectl run nprod1 --image=nginx --labels=env=prod
>kubectl run nprod2 --image=nginx --labels=env=prod
```
### Q3:
Verify all the pods are created with correct labels
### Answer3:
```yaml
>kubectl get pods --show-labels
NAME                            READY   STATUS    RESTARTS   AGE    LABELS
hr-web-app-99dfd4c9d-9t8sz      1/1     Running   0          116s   app=hr-web-app,pod-template-hash=99dfd4c9d
hr-web-app-99dfd4c9d-bpt4v      1/1     Running   0          116s   app=hr-web-app,pod-template-hash=99dfd4c9d
ndev1                           1/1     Running   0          40s    env=dev
ndev2                           1/1     Running   0          34s    env=dev
ndev3                           1/1     Running   0          29s    env=dev
nginx-deploy-6c858c4486-rpnwz   1/1     Running   0          115s   app=nginx-deploy,pod-template-hash=6c858c4486
nprod1                          1/1     Running   0          22s    env=prod
nprod2                          1/1     Running   0          17s    env=prod
```
### Q4:
Get the pods with label env=dev
### Answer4:
```yaml
>kubectl get pods -l env=dev
NAME    READY   STATUS    RESTARTS   AGE
ndev1   1/1     Running   0          106s
ndev2   1/1     Running   0          100s
ndev3   1/1     Running   0          95s
```
### Q5:
Get the pods with label env=dev and also output the labels
### Answer5:
```yaml
>kubectl get pods -l env=dev --show-labels
NAME    READY   STATUS    RESTARTS   AGE     LABELS
ndev1   1/1     Running   0          3m45s   env=dev
ndev2   1/1     Running   0          3m39s   env=dev
ndev3   1/1     Running   0          3m34s   env=dev
```
### Q6:
Get the pods with label env=prod
### Answer6:
```yaml
>kubectl get pods -l env=prod
NAME     READY   STATUS    RESTARTS   AGE
nprod1   1/1     Running   0          5m15s
nprod2   1/1     Running   0          5m10s
```

### Q7:
Get the pods with label env=prod and also output the labels
### Answer7:
```yaml
>kubectl get pods -l env=prod --show-labels
NAME     READY   STATUS    RESTARTS   AGE     LABELS
nprod1   1/1     Running   0          5m59s   env=prod
nprod2   1/1     Running   0          5m54s   env=prod
```
### Q8:
Get the pods with label env
### Answer8:
```yaml
>kubectl get pods -L env
NAME                            READY   STATUS    RESTARTS   AGE     ENV
hr-web-app-99dfd4c9d-9t8sz      1/1     Running   0          8m12s
hr-web-app-99dfd4c9d-bpt4v      1/1     Running   0          8m12s
ndev1                           1/1     Running   0          6m56s   dev
ndev2                           1/1     Running   0          6m50s   dev
ndev3                           1/1     Running   0          6m45s   dev
nginx-deploy-6c858c4486-rpnwz   1/1     Running   0          8m11s
nprod1                          1/1     Running   0          6m38s   prod
nprod2                          1/1     Running   0          6m33s   prod
```
### Q9:
Get the pods with labels env=dev and env=prod
### Answer9:
```yaml
kubectl get pods -l 'env in (dev,prod)'
```
### Q10:
Get the pods with labels env=dev and env=prod and output the labels as well
### Answer9:
```yaml
kubectl get pods -l 'env in (dev,prod)' --show-labels
```
### Q11:
Change the label for one of the pod to env=uat and list all the pods to verify

### Answer11:
```yaml
>kubectl label pod/ndev3 env=uat --overwrite
pod/ndev3 labeled

>kubectl get pods --show-labels
NAME                            READY   STATUS    RESTARTS   AGE   LABELS
hr-web-app-99dfd4c9d-9t8sz      1/1     Running   0          26m   app=hr-web-app,pod-template-hash=99dfd4c9d
hr-web-app-99dfd4c9d-bpt4v      1/1     Running   0          26m   app=hr-web-app,pod-template-hash=99dfd4c9d
ndev1                           1/1     Running   0          25m   env=dev
ndev2                           1/1     Running   0          25m   env=dev
ndev3                           1/1     Running   0          24m   env=uat
nginx-deploy-6c858c4486-rpnwz   1/1     Running   0          26m   app=nginx-deploy,pod-template-hash=6c858c4486
nprod1                          1/1     Running   0          24m   env=prod

```
### Q12:
Remove the labels for the pods that we created now and verify all the labels are removed

### Answer12:
```yaml
>kubectl label pod ndev1 env-
pod/ndev1 labeled

>kubectl label pod ndev2 env-
pod/ndev2 labeled

>kubectl label pod ndev3 env-
pod/ndev3 labeled

>kubectl label pod nprod1 env-
pod/nprod1 labeled

>kubectl label pod nprod2 env-
pod/nprod2 labeled

>kubectl get pod --show-labels
NAME                            READY   STATUS    RESTARTS   AGE   LABELS
hr-web-app-99dfd4c9d-9t8sz      1/1     Running   0          42m   app=hr-web-app,pod-template-hash=99dfd4c9d
hr-web-app-99dfd4c9d-bpt4v      1/1     Running   0          42m   app=hr-web-app,pod-template-hash=99dfd4c9d
ndev1                           1/1     Running   0          41m   app=nginx
ndev2                           1/1     Running   0          41m   <none>
ndev3                           1/1     Running   0          41m   <none>
nginx-deploy-6c858c4486-rpnwz   1/1     Running   0          42m   app=nginx-deploy,pod-template-hash=6c858c4486
nprod1                          1/1     Running   0          40m   <none>
nprod2                          1/1     Running   0          40m   <none>
```
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
