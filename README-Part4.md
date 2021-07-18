## Part3

### Q1:
Create a file called config.txt with two values key1=value1 and key2=value2 and
verify the file:

cat >> config.txt << EOF
key1=value1
key2=value2
EOF
cat config

### Answer1:

```yaml
>echo key1=value1 > config.txt
>echo key2=value2 >> config.txt
>echo EOF >> config.txt
```

### Q2:
Create a configmap named keyvalcfgmap and read data from the file config.txt and
verify that configmap is created correctly

### Answer2:
```yaml
>kubectl create cm keyvalcfgmap --from-file=config.txt
configmap/keyvalcfgmap created

>kubectl get cm keyvalcfgmap -o yaml
apiVersion: v1
data:
  config.txt: "key1=value1 \r\nkey2=value2 \r\nEOF \r\n"
kind: ConfigMap
metadata:
  creationTimestamp: "2021-07-18T06:50:34Z"
  name: keyvalcfgmap
  namespace: default
  resourceVersion: "35631"
  uid: cfb5984c-10e9-4549-a84e-5368d7cfc4c5

```
### Q3:
Create an nginx pod and load environment values from the above configmap
keyvalcfgmap and exec into the pod and verify the environment variables and delete
the pod
// first run this command to save the pod yml
kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml > nginx-pod.yml

### Answer3:
```yaml
>kubectl run nginx --image=nginx --restart=Never -o yaml > nginx-pod.yml

>kubectl create -f nginx-pod.yml

Verify:
>kubectl exec -it nginx -- env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=nginx
TERM=xterm
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_SERVICE_HOST=10.96.0.1
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
NGINX_RESOLVER_SERVICE_PORT=tcp://10.110.60.238:80
NGINX_RESOLVER_SERVICE_PORT_80_TCP_PORT=80
KUBERNETES_SERVICE_PORT=443
NGINX_RESOLVER_SERVICE_PORT_80_TCP_PROTO=tcp
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT=tcp://10.96.0.1:443
NGINX_RESOLVER_SERVICE_SERVICE_HOST=10.110.60.238
NGINX_RESOLVER_SERVICE_SERVICE_PORT=80
NGINX_RESOLVER_SERVICE_PORT_80_TCP=tcp://10.110.60.238:80
NGINX_RESOLVER_SERVICE_PORT_80_TCP_ADDR=10.110.60.238
NGINX_VERSION=1.21.1
NJS_VERSION=0.6.1
PKG_RELEASE=1~buster
HOME=/root

>kubectl delete po nginx
pod "nginx" deleted
```
