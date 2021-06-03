# Helm

View Helm environment variables
```shell
helm env
```

## Installing a chart from public chart repositories

Count how many Helm charts are on in [Artifact Hub](https://artifacthub.io/)
```shell
echo "The number of charts on Artifact Hub is: $(helm search hub | wc -l)."
```

Search for a specific chart
```shell
helm search hub redis
```

List of some popular charts
```shell
helm search hub postgres
helm search hub sonarqube
helm search hub rabbitmq
helm search hub kafka
helm search hub prometheus-operator
helm search hub tensorflow
helm search hub tekton
```

Add a repo other than [Artifact Hub](https://artifacthub.io/) to the local Helm cache
```shell
helm repo add bitnami https://charts.bitnami.com/bitnami
```

List local repos
```shell
helm repo list
```

Commands for getting info about a specific repo or chart
```shell
helm search repo bitnami/redis
helm show chart bitnami/redis
helm show readme bitnami/redis
helm show values bitnami/redis
```

Install a chart (bitnami/redis) to a cluster (namespace redis).
The Kubernetes redis namespace must already exist.
```shell
helm install my-redis bitnami/redis version 10.7.16 --namespace redis
```

## Managing charts

List Kubernetes namespaces
```shell
helm list --all-namespaces
helm ls -n redis
```

List Helm charts
```shell
helm list -A
```

Delete a deployed chart
```shell
helm delete my-redis -n redis
```

## Creating a chart

Create a chart that has name 'app-chart'
```shell
helm create app-chart
```

Dry run the installation
```shell
helm install my-app ./app-chart --dry-run --debug
```

Dry run, setting non-default property value
```shell
helm install my-app ./app-chart --dry-run --debug --set image.pullPolicy=Always
```

Deploy a chart
```shell
helm install my-app ./app-chart --set image.pullPolicy=Always
```

List apps/deployments
```shell
helm list
kubectl get deployments,service
```

Change service type to NodePort
```shell
helm upgrade my-app ./app-chart --install --reuse-values --set service.type=NodePort
# Patch config to expose Nginx port 31111
kubectl patch service my-app-app-chart --type='json' --patch='[{"op": "replace", "path": "/spec/ports/0/nodePort", "value":31111}]'
```

Other helpful commands
```shell
helm lint
helm test
```

## Helm repositories
[Artifact Hub](https://artifacthub.io/)  
[ChartMuseum](https://github.com/helm/chartmuseum) # deploy as your own chart repository

## Helm plugins
[The Helm Plugins Guide](https://helm.sh/docs/topics/plugins/)
[Curated Helm Plugins](https://helm.sh/docs/community/related/)







