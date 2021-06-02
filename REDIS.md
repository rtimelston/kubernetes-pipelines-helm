# Redis

Ping a Redis instance deployed by [Helm](./HELM.md) on [Kubernetes](./KUBERNETES.md)
```shell
redis-cli -h 127.0.0.1 -p 6379 -a $REDIS_PASSWORD ping
```





