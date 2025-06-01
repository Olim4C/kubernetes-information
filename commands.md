# Comando utiles de kubernetes

### comandos varios
```bash 
kubectl run <pod_name> --image=<dockerimage>
```
```bash 
kubectl run <pod_name> --image=<dockerimage> --dry-run=client -o yaml
```
```bash 
kubectl edit pod 
```
```bash 
kubectl describe <resource> <resource_name>
```

```bash
kubectl replace -f <nombre_yaml_file_manifiesto>
```
```bash
kubectl scale --replicas=<cantidad_deseada> -f <nombre_yaml_file_manifiesto>
```
```bash
kubectl scale --replicas=<> replicaset <replicaset_nombre>
```

```bash
kubectl create -f <nombre_yaml_file_manifiesto>
```
```bash
kubectl create deployment --image=<dockerimage> <deployment_name>
```
```bash
kubectl create deployment --image=<dockerimage> <deployment_name> --dry-run=client -o yaml
```
```bash
kubectl create deployment --image=<dockerimage> <deployment_name> --replicas=4 --dry-run=client -o yaml
```
```bash
kubectl create configmap <configmap_name> --from-file=<file_directory>
```
```bash
kubectl delete -f <nombre_yaml_file_manifiesto>
```

```bash
kubectl get pod --selector type=front-end
```
```bash
kubectl explain <objeto_de_kubernetes>
```

### comando imperativos en kubernetes
```bash
kubectl run --image=<dockerimage> nginx
```
```bash
kubectl create deployment --image=<dockerimage> nginx
```
```bash
kubectl expose deployment nginx --port 80
```
```bash
kubectl edit deployment nginx
```
```bash
kubectl scale deployment nginx --replicas=5
```
```bash
kubectl set image deployment nginx nginx=<dockerimage>:1.18
```
```bash
kubectl create -f nginx.yaml
```
```bash
kubectl replace -f nginx.yaml
```
```bash
kubectl delete -f nginx.yaml
```

### comando declarativos en kubernetes
```bash
kubectl apply -f nginx.yaml
```

# Static Pods

## kubelet.service

### Option1
```bash
ExecStart=/usr/local/bin/kubelet \\
    --container-runtime=remote \\
    --container-runtime-endpoint=unix:///var/run/containerd/containerd.sock \\
    --pod-manifest-path=/etc/kubernetes/manifest \\
    --kubeconfig=/var/lib/kubelet/kubeconfig \\
    --network-plugin=cni \\
    --register-node=true \\
    --v=2
```

### Option 2
```bash
ExecStart=/usr/local/bin/kubelet \\
    --container-runtime=remote \\
    --container-runtime-endpoint=unix:///var/run/containerd/containerd.sock \\
    --config=kubeconfig.yaml \\
    --kubeconfig=/var/lib/kubelet/kubeconfig \\
    --network-plugin=cni \\
    --register-node=true \\
    --v=2
```
when we use this option we have to configure the kubeconfig.yaml
```yaml
staticPodPath: /etc/kubernetes/manifest
```

## Static Pod vs DaemonSets
| Static PODs | DaemonSets |
|-------------|------------|
| Created by the kubelet | Created by the kube-API server (DaemonSet Controller) |
| Deploy Control Plane components as Static Pods | Deploy Monitoring Agents, Logging Agents on nodes |
| **Ignored by the Kube-scheduler** | **Ignored by the Kube-scheduler** |

## Cluster maintenance

Drain a node and move the pods to another node and make the current node not schedule new pods
```bash
kubectl drain <node_name>
```

uncordon a node and make it as schedulable
```bash
kubectl uncordon <node_name>
```

cordon a node to avoid scheduling new pods in that node
```bash
kubectl cordon <node_name>
```

switch clusters
```bash
kubectl config use-context <cluster_name>
```

## Certificates

### Create certificates
To create a certificate you have to follow the following steps

1. **Generate a key**
```bash
openssl genrsa -out ca.key 2048
```

2. **Generate a Certificate Signing Request (We have to specify the key created before)**
```bash
openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr
```

3. **Sign Certificates (We have to specify the Signing Request and the key)**
```bash
openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt
```


### Get more information about certain certificate
```bash
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -test -noout
```

### Inspect Logs

```bash
kubectl logs etcd-master
```
