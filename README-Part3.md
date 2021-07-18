## Part3

### Q1:
1. Create a deployment called webapp with image nginx with 5 replicas
 a. Use the below command to create a yaml file.
 i. kubectl create deploy webapp --image=nginx --dry-run -o yaml > webapp.yaml
ii. Edit it and add 5 replica’s
### Answer1:
[webapp.yaml](/webapp.yaml)

```yaml
>kubectl create -f webapp.yaml
deployment.apps/webapp created
```

### Q2:
Get the deployment rollout status
### Answer2:
```yaml
>kubectl rollout status deploy webapp
deployment "webapp" successfully rolled out

```
### Q3:
Get the replicaset that created with this deployment
### Answer3:
```yaml
>kubectl get rs -l app=webapp
NAME               DESIRED   CURRENT   READY   AGE
webapp-5654c984c   5         5         5       8m38s
```
### Q4:
EXPORT the yaml of the replicaset and pods of this deployment
### Answer4:
```yaml
>kubectl get rs -l app=webapp -o yaml
apiVersion: v1
items:
- apiVersion: apps/v1
  kind: ReplicaSet
  metadata:
    annotations:
      deployment.kubernetes.io/desired-replicas: "5"
      deployment.kubernetes.io/max-replicas: "7"
      deployment.kubernetes.io/revision: "1"
    creationTimestamp: "2021-07-17T20:42:48Z"
    generation: 1
    labels:
      app: webapp
      pod-template-hash: 5654c984c
    name: webapp-5654c984c
    namespace: default
    ownerReferences:
    - apiVersion: apps/v1
      blockOwnerDeletion: true
      controller: true
      kind: Deployment
      name: webapp
      uid: 5b75caaf-58c4-4309-a992-4a52df6bbef4
    resourceVersion: "30535"
    uid: 4217a718-7a8c-4f41-9fa1-17df5faacd83
  spec:
    replicas: 5
    selector:
      matchLabels:
        app: webapp
        pod-template-hash: 5654c984c
    template:
      metadata:
        creationTimestamp: null
        labels:
          app: webapp
          pod-template-hash: 5654c984c
      spec:
        containers:
        - image: nginx
          imagePullPolicy: Always
          name: nginx
          resources: {}
          terminationMessagePath: /dev/termination-log
          terminationMessagePolicy: File
        dnsPolicy: ClusterFirst
        restartPolicy: Always
        schedulerName: default-scheduler
        securityContext: {}
        terminationGracePeriodSeconds: 30
  status:
    availableReplicas: 5
    fullyLabeledReplicas: 5
    observedGeneration: 1
    readyReplicas: 5
    replicas: 5
kind: List
metadata:
  resourceVersion: ""
  selfLink: ""
  
kubectl get po -l app=webapp -o yaml
apiVersion: v1
items:
- apiVersion: v1
  kind: Pod
  metadata:
    creationTimestamp: "2021-07-17T20:42:48Z"
    generateName: webapp-5654c984c-
    labels:
      app: webapp
      pod-template-hash: 5654c984c
    name: webapp-5654c984c-bj9np
    namespace: default
    ownerReferences:
    - apiVersion: apps/v1
      blockOwnerDeletion: true
      controller: true
      kind: ReplicaSet
      name: webapp-5654c984c
      uid: 4217a718-7a8c-4f41-9fa1-17df5faacd83
    resourceVersion: "30519"
    uid: 0865dd56-5add-4163-b7c9-adcca3740998
  spec:
    containers:
    - image: nginx
      imagePullPolicy: Always
      name: nginx
      resources: {}
      terminationMessagePath: /dev/termination-log
      terminationMessagePolicy: File
      volumeMounts:
      - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
        name: kube-api-access-nhznp
        readOnly: true
    dnsPolicy: ClusterFirst
    enableServiceLinks: true
    nodeName: minikube
    preemptionPolicy: PreemptLowerPriority
    priority: 0
    restartPolicy: Always
    schedulerName: default-scheduler
    securityContext: {}
    serviceAccount: default
    serviceAccountName: default
    terminationGracePeriodSeconds: 30
    tolerations:
    - effect: NoExecute
      key: node.kubernetes.io/not-ready
      operator: Exists
      tolerationSeconds: 300
    - effect: NoExecute
      key: node.kubernetes.io/unreachable
      operator: Exists
      tolerationSeconds: 300
    volumes:
    - name: kube-api-access-nhznp
      projected:
        defaultMode: 420
        sources:
        - serviceAccountToken:
            expirationSeconds: 3607
            path: token
        - configMap:
            items:
            - key: ca.crt
              path: ca.crt
            name: kube-root-ca.crt
        - downwardAPI:
            items:
            - fieldRef:
                apiVersion: v1
                fieldPath: metadata.namespace
              path: namespace
  status:
    conditions:
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:48Z"
      status: "True"
      type: Initialized
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:58Z"
      status: "True"
      type: Ready
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:58Z"
      status: "True"
      type: ContainersReady
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:48Z"
      status: "True"
      type: PodScheduled
    containerStatuses:
    - containerID: docker://bb2006512201410d318e6622fdeb95091c910fb6d40344f116cf63a9553018c9
      image: nginx:latest
      imageID: docker-pullable://nginx@sha256:353c20f74d9b6aee359f30e8e4f69c3d7eaea2f610681c4a95849a2fd7c497f9
      lastState: {}
      name: nginx
      ready: true
      restartCount: 0
      started: true
      state:
        running:
          startedAt: "2021-07-17T20:42:57Z"
    hostIP: 192.168.99.101
    phase: Running
    podIP: 172.17.0.17
    podIPs:
    - ip: 172.17.0.17
    qosClass: BestEffort
    startTime: "2021-07-17T20:42:48Z"
- apiVersion: v1
  kind: Pod
  metadata:
    creationTimestamp: "2021-07-17T20:42:48Z"
    generateName: webapp-5654c984c-
    labels:
      app: webapp
      pod-template-hash: 5654c984c
    name: webapp-5654c984c-czwfx
    namespace: default
    ownerReferences:
    - apiVersion: apps/v1
      blockOwnerDeletion: true
      controller: true
      kind: ReplicaSet
      name: webapp-5654c984c
      uid: 4217a718-7a8c-4f41-9fa1-17df5faacd83
    resourceVersion: "30527"
    uid: 2ad407cd-3e01-4060-86d6-ba00a8dc1ce8
  spec:
    containers:
    - image: nginx
      imagePullPolicy: Always
      name: nginx
      resources: {}
      terminationMessagePath: /dev/termination-log
      terminationMessagePolicy: File
      volumeMounts:
      - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
        name: kube-api-access-jlkvs
        readOnly: true
    dnsPolicy: ClusterFirst
    enableServiceLinks: true
    nodeName: minikube
    preemptionPolicy: PreemptLowerPriority
    priority: 0
    restartPolicy: Always
    schedulerName: default-scheduler
    securityContext: {}
    serviceAccount: default
    serviceAccountName: default
    terminationGracePeriodSeconds: 30
    tolerations:
    - effect: NoExecute
      key: node.kubernetes.io/not-ready
      operator: Exists
      tolerationSeconds: 300
    - effect: NoExecute
      key: node.kubernetes.io/unreachable
      operator: Exists
      tolerationSeconds: 300
    volumes:
    - name: kube-api-access-jlkvs
      projected:
        defaultMode: 420
        sources:
        - serviceAccountToken:
            expirationSeconds: 3607
            path: token
        - configMap:
            items:
            - key: ca.crt
              path: ca.crt
            name: kube-root-ca.crt
        - downwardAPI:
            items:
            - fieldRef:
                apiVersion: v1
                fieldPath: metadata.namespace
              path: namespace
  status:
    conditions:
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:48Z"
      status: "True"
      type: Initialized
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:43:00Z"
      status: "True"
      type: Ready
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:43:00Z"
      status: "True"
      type: ContainersReady
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:48Z"
      status: "True"
      type: PodScheduled
    containerStatuses:
    - containerID: docker://5bedd8a919bfc513b7c7351b19abeac723d9b38f2af92e675de7c9a44f440969
      image: nginx:latest
      imageID: docker-pullable://nginx@sha256:353c20f74d9b6aee359f30e8e4f69c3d7eaea2f610681c4a95849a2fd7c497f9
      lastState: {}
      name: nginx
      ready: true
      restartCount: 0
      started: true
      state:
        running:
          startedAt: "2021-07-17T20:42:59Z"
    hostIP: 192.168.99.101
    phase: Running
    podIP: 172.17.0.19
    podIPs:
    - ip: 172.17.0.19
    qosClass: BestEffort
    startTime: "2021-07-17T20:42:48Z"
- apiVersion: v1
  kind: Pod
  metadata:
    creationTimestamp: "2021-07-17T20:42:48Z"
    generateName: webapp-5654c984c-
    labels:
      app: webapp
      pod-template-hash: 5654c984c
    name: webapp-5654c984c-qgsk5
    namespace: default
    ownerReferences:
    - apiVersion: apps/v1
      blockOwnerDeletion: true
      controller: true
      kind: ReplicaSet
      name: webapp-5654c984c
      uid: 4217a718-7a8c-4f41-9fa1-17df5faacd83
    resourceVersion: "30512"
    uid: 0cd6b46e-f235-4a20-bf36-3da7335b4aa3
  spec:
    containers:
    - image: nginx
      imagePullPolicy: Always
      name: nginx
      resources: {}
      terminationMessagePath: /dev/termination-log
      terminationMessagePolicy: File
      volumeMounts:
      - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
        name: kube-api-access-cg6gt
        readOnly: true
    dnsPolicy: ClusterFirst
    enableServiceLinks: true
    nodeName: minikube
    preemptionPolicy: PreemptLowerPriority
    priority: 0
    restartPolicy: Always
    schedulerName: default-scheduler
    securityContext: {}
    serviceAccount: default
    serviceAccountName: default
    terminationGracePeriodSeconds: 30
    tolerations:
    - effect: NoExecute
      key: node.kubernetes.io/not-ready
      operator: Exists
      tolerationSeconds: 300
    - effect: NoExecute
      key: node.kubernetes.io/unreachable
      operator: Exists
      tolerationSeconds: 300
    volumes:
    - name: kube-api-access-cg6gt
      projected:
        defaultMode: 420
        sources:
        - serviceAccountToken:
            expirationSeconds: 3607
            path: token
        - configMap:
            items:
            - key: ca.crt
              path: ca.crt
            name: kube-root-ca.crt
        - downwardAPI:
            items:
            - fieldRef:
                apiVersion: v1
                fieldPath: metadata.namespace
              path: namespace
  status:
    conditions:
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:48Z"
      status: "True"
      type: Initialized
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:56Z"
      status: "True"
      type: Ready
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:56Z"
      status: "True"
      type: ContainersReady
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:48Z"
      status: "True"
      type: PodScheduled
    containerStatuses:
    - containerID: docker://be4df92367874e425ed83fe7e8b2230b4fce794711af787b5f1d5a72bca0da6e
      image: nginx:latest
      imageID: docker-pullable://nginx@sha256:353c20f74d9b6aee359f30e8e4f69c3d7eaea2f610681c4a95849a2fd7c497f9
      lastState: {}
      name: nginx
      ready: true
      restartCount: 0
      started: true
      state:
        running:
          startedAt: "2021-07-17T20:42:55Z"
    hostIP: 192.168.99.101
    phase: Running
    podIP: 172.17.0.16
    podIPs:
    - ip: 172.17.0.16
    qosClass: BestEffort
    startTime: "2021-07-17T20:42:48Z"
- apiVersion: v1
  kind: Pod
  metadata:
    creationTimestamp: "2021-07-17T20:42:48Z"
    generateName: webapp-5654c984c-
    labels:
      app: webapp
      pod-template-hash: 5654c984c
    name: webapp-5654c984c-xmztt
    namespace: default
    ownerReferences:
    - apiVersion: apps/v1
      blockOwnerDeletion: true
      controller: true
      kind: ReplicaSet
      name: webapp-5654c984c
      uid: 4217a718-7a8c-4f41-9fa1-17df5faacd83
    resourceVersion: "30534"
    uid: 27c8df38-b455-48cb-aa4b-8c63212d0e62
  spec:
    containers:
    - image: nginx
      imagePullPolicy: Always
      name: nginx
      resources: {}
      terminationMessagePath: /dev/termination-log
      terminationMessagePolicy: File
      volumeMounts:
      - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
        name: kube-api-access-lj6r6
        readOnly: true
    dnsPolicy: ClusterFirst
    enableServiceLinks: true
    nodeName: minikube
    preemptionPolicy: PreemptLowerPriority
    priority: 0
    restartPolicy: Always
    schedulerName: default-scheduler
    securityContext: {}
    serviceAccount: default
    serviceAccountName: default
    terminationGracePeriodSeconds: 30
    tolerations:
    - effect: NoExecute
      key: node.kubernetes.io/not-ready
      operator: Exists
      tolerationSeconds: 300
    - effect: NoExecute
      key: node.kubernetes.io/unreachable
      operator: Exists
      tolerationSeconds: 300
    volumes:
    - name: kube-api-access-lj6r6
      projected:
        defaultMode: 420
        sources:
        - serviceAccountToken:
            expirationSeconds: 3607
            path: token
        - configMap:
            items:
            - key: ca.crt
              path: ca.crt
            name: kube-root-ca.crt
        - downwardAPI:
            items:
            - fieldRef:
                apiVersion: v1
                fieldPath: metadata.namespace
              path: namespace
  status:
    conditions:
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:48Z"
      status: "True"
      type: Initialized
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:43:02Z"
      status: "True"
      type: Ready
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:43:02Z"
      status: "True"
      type: ContainersReady
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:48Z"
      status: "True"
      type: PodScheduled
    containerStatuses:
    - containerID: docker://22aefb4f832e76a6f6a9d9d4b6863ac9eb4b6c89ec3088477cc24e1251a9817f
      image: nginx:latest
      imageID: docker-pullable://nginx@sha256:353c20f74d9b6aee359f30e8e4f69c3d7eaea2f610681c4a95849a2fd7c497f9
      lastState: {}
      name: nginx
      ready: true
      restartCount: 0
      started: true
      state:
        running:
          startedAt: "2021-07-17T20:43:01Z"
    hostIP: 192.168.99.101
    phase: Running
    podIP: 172.17.0.18
    podIPs:
    - ip: 172.17.0.18
    qosClass: BestEffort
    startTime: "2021-07-17T20:42:48Z"
- apiVersion: v1
  kind: Pod
  metadata:
    creationTimestamp: "2021-07-17T20:42:48Z"
    generateName: webapp-5654c984c-
    labels:
      app: webapp
      pod-template-hash: 5654c984c
    name: webapp-5654c984c-zlfp8
    namespace: default
    ownerReferences:
    - apiVersion: apps/v1
      blockOwnerDeletion: true
      controller: true
      kind: ReplicaSet
      name: webapp-5654c984c
      uid: 4217a718-7a8c-4f41-9fa1-17df5faacd83
    resourceVersion: "30505"
    uid: d52ca27a-4aa3-4c1d-94fc-bd6035d7fff9
  spec:
    containers:
    - image: nginx
      imagePullPolicy: Always
      name: nginx
      resources: {}
      terminationMessagePath: /dev/termination-log
      terminationMessagePolicy: File
      volumeMounts:
      - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
        name: kube-api-access-87xxz
        readOnly: true
    dnsPolicy: ClusterFirst
    enableServiceLinks: true
    nodeName: minikube
    preemptionPolicy: PreemptLowerPriority
    priority: 0
    restartPolicy: Always
    schedulerName: default-scheduler
    securityContext: {}
    serviceAccount: default
    serviceAccountName: default
    terminationGracePeriodSeconds: 30
    tolerations:
    - effect: NoExecute
      key: node.kubernetes.io/not-ready
      operator: Exists
      tolerationSeconds: 300
    - effect: NoExecute
      key: node.kubernetes.io/unreachable
      operator: Exists
      tolerationSeconds: 300
    volumes:
    - name: kube-api-access-87xxz
      projected:
        defaultMode: 420
        sources:
        - serviceAccountToken:
            expirationSeconds: 3607
            path: token
        - configMap:
            items:
            - key: ca.crt
              path: ca.crt
            name: kube-root-ca.crt
        - downwardAPI:
            items:
            - fieldRef:
                apiVersion: v1
                fieldPath: metadata.namespace
              path: namespace
  status:
    conditions:
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:48Z"
      status: "True"
      type: Initialized
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:53Z"
      status: "True"
      type: Ready
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:53Z"
      status: "True"
      type: ContainersReady
    - lastProbeTime: null
      lastTransitionTime: "2021-07-17T20:42:48Z"
      status: "True"
      type: PodScheduled
    containerStatuses:
    - containerID: docker://956fc5aea50cd2540208b08c6adca977225499bf2ae21a687a6d63c89583b08c
      image: nginx:latest
      imageID: docker-pullable://nginx@sha256:353c20f74d9b6aee359f30e8e4f69c3d7eaea2f610681c4a95849a2fd7c497f9
      lastState: {}
      name: nginx
      ready: true
      restartCount: 0
      started: true
      state:
        running:
          startedAt: "2021-07-17T20:42:53Z"
    hostIP: 192.168.99.101
    phase: Running
    podIP: 172.17.0.15
    podIPs:
    - ip: 172.17.0.15
    qosClass: BestEffort
    startTime: "2021-07-17T20:42:48Z"
kind: List
metadata:
  resourceVersion: ""
  selfLink: "" 

```
### Q5:
Delete the deployment you just created and watch all the pods are also being deleted
### Answer5:
```yaml
>kubectl delete deploy webapp
deployment.apps "webapp" deleted

>kubectl get po -l app=webapp -w

```
### Q6:
Create a deployment of webapp with image nginx:1.17.1 with container port 80 and verify the image version
a. kubectl create deploy webapp --image=nginx:1.17.1 --dry-run -o yaml > webapp.yaml
b. add the port section (80)
### Answer6:
[webapp2.yaml](/webapp2.yaml)

```yaml
>kubectl create -f webapp2.yaml

verify the image version:
kubectl describe deploy webapp | grep Image
```

### Q7:
Update the deployment with the image version 1.17.4 and verify
### Answer7:
```yaml
>kubectl set image deploy/webapp nginx=nginx:1.17.4
deployment.apps/webapp image updated

verify the image:
>kubectl describe deploy webapp | grep Image

```
### Q8:
Check the rollout history and make sure everything is ok after the update
### Answer8:
```yaml
>kubectl rollout history deploy webapp
deployment.apps/webapp
REVISION  CHANGE-CAUSE
1         <none>
2         <none>

>kubectl get deploy webapp --show-labels
NAME     READY   UP-TO-DATE   AVAILABLE   AGE   LABELS
webapp   1/1     1            1           12m   app=webapp

>kubectl get rs -l app=webapp
NAME                DESIRED   CURRENT   READY   AGE
webapp-6c98f678d9   0         0         0       12m
webapp-7d88bcbdcd   1         1         1       5m11s

>kubectl get po -l app=webapp
NAME                      READY   STATUS    RESTARTS   AGE
webapp-7d88bcbdcd-79x7h   1/1     Running   0          5m38s
```
### Q9:
Undo the deployment to the previous version 1.17.1 and verify Image has the previous version
### Answer9:
```yaml
>kubectl rollout undo deploy webapp
deployment.apps/webapp rolled back

verify:
>kubectl describe deploy webapp | grep Image

```
### Q10:
Update the deployment with the wrong image version 1.100 and verify something is
wrong with the deployment
a. Expect: kubectl get pods (ImagePullErr)
b. Undo the deployment with the previous version and verify everything is Ok
c. kubectl rollout history deploy webapp --revision=7
d. Check the history of the specific revision of that deployment
e. update the deployment with the image version latest and check the history
and verify nothing is going on

### Answer10:
```yaml
>kubectl set image deploy/webapp nginx=nginx:1.100
deployment.apps/webapp image updated

>kubectl rollout status deploy webapp
Waiting for deployment "webapp" rollout to finish: 1 old replicas are pending termination...

>kubectl get pods
NAME                            READY   STATUS             RESTARTS   AGE
webapp-6c98f678d9-7hpmc         1/1     Running            0          4m48s
webapp-6cc75f59b9-9krk4         0/1     ImagePullBackOff   0          2m37s

>kubectl rollout undo deploy webapp
deployment.apps/webapp rolled back

>kubectl rollout status deploy webapp
Waiting for deployment "webapp" rollout to finish: 1 old replicas are pending termination...

>kubectl get pods
NAME                            READY   STATUS         RESTARTS   AGE
webapp-6c98f678d9-7hpmc         1/1     Running        0          8m5s
webapp-6cc75f59b9-dph58         0/1     ErrImagePull   0          67s

>kubectl rollout history deploy webapp --revision=7
error: unable to find the specified revision

>kubectl rollout pause deploy webapp
deployment.apps/webapp paused

>kubectl set image deploy/webapp nginx=nginx:latest
deployment.apps/webapp image updated

>kubectl rollout history deploy webapp
deployment.apps/webapp
REVISION  CHANGE-CAUSE
2         <none>
5         <none>
6         <none>

```
### Q11:
Apply the autoscaling to this deployment with minimum 10 and maximum 20 replicas
and target CPU of 85% and verify hpa is created and replicas are increased to 10 from 1
### Answer11:
```yaml
>kubectl autoscale deploy webapp --min=10 --max=20 --cpu-percent=85
horizontalpodautoscaler.autoscaling/webapp autoscaled

>kubectl get hpa
NAME     REFERENCE           TARGETS         MINPODS   MAXPODS   REPLICAS   AGE
webapp   Deployment/webapp   <unknown>/85%   10        20        1          24s

>kubectl get pod -l app=webapp
NAME                      READY   STATUS             RESTARTS   AGE
webapp-6c98f678d9-4jq57   1/1     Running            0          31s
webapp-6c98f678d9-7hpmc   1/1     Running            0          13m
webapp-6c98f678d9-bv9rk   1/1     Running            0          31s
webapp-6c98f678d9-j9kms   1/1     Running            0          31s
webapp-6c98f678d9-xqqzn   1/1     Running            0          31s
webapp-6c98f678d9-xv967   1/1     Running            0          31s
webapp-6cc75f59b9-blqhv   0/1     ErrImagePull       0          31s
webapp-6cc75f59b9-dph58   0/1     ImagePullBackOff   0          6m38s
webapp-6cc75f59b9-hnj6q   0/1     ImagePullBackOff   0          31s
webapp-6cc75f59b9-qq5tf   0/1     ImagePullBackOff   0          31s
webapp-6cc75f59b9-x46lg   0/1     ImagePullBackOff   0          31s
webapp-6cc75f59b9-xdc7k   0/1     ErrImagePull       0          31s
webapp-6cc75f59b9-zms6d   0/1     ImagePullBackOff   0          31s

```
### Q12:
No question ;)
### Answer12:
```yaml
There is nothing to write here...
```
### Q13:
Clean the cluster by deleting deployment and hpa you just created
### Answer13:
```yaml
>kubectl delete deploy webapp
deployment.apps "webapp" deleted

>kubectl delete hpa webapp
horizontalpodautoscaler.autoscaling "webapp" deleted

```
### Q14:
Create a job and make it run 10 times one after one (run > exit > run >exit ..) using
the following configuration:
kubectl create job hello-job --image=busybox --dry-run -o yaml -- echo "Hello I am
from job" > hello-job.yaml”
a. Add to the above job completions: 10 inside the yaml
### Answer14:
```yaml
>kubectl create job hello-job --image=busybox -o yaml -- echo "Hello I am from job" > hello-job.yaml


```
