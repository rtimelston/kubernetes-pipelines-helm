# Kubernetes

## Validate Kubernetes installation
```shell
kubectl version --short && \
> kubectl get componentstatus && \
> kubectl get nodes && \
> kubectl cluster-info
```

## Commands
Create a namespace for the installation target
```shell
kubectl create namespace redis
```

List Helm secrets
```shell
kubectl get secrets --all-namespaces | grep sh.helm
kubctl get secrets --all-namespaces --selector owner=helm
```

Describe secret information about a deployed chart
```shell
kubectl --namepace redis describe secret sh.helm.release.v1.my-redis.v1
```

Create a persistent volume (here, for redis)
```shell
kubectl apply -f pv.yaml
# Make sure Redis can write to mount points
mkdir /mnt/data1 /mnt/data2 /mt/data3 --mode=777
# Monitor progress from Pending to Running state
watch kubectl get statefulsets,pods,services -n redis
# Ctrl+C to exit watch
```

Get a server password from an installed bitnami/redis chart
```shell
export REDIS_PASSWORD=$(kubectl get secret --namespace redis my-redis -o jsonpath="{.data.redis-password}" | base64 --decode)
```

Expose the Redis master service on port 6379
```shell
kubectl port-forward --namespace redis service/my-redis-master 6379:6379 > /dev/null &
```

Delete a persistent volume by name
```shell
kubectl delete persistentvolume pv-volume3
```

Delete a namespace
```shell
kubectl delete namespace redis
```







