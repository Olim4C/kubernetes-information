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