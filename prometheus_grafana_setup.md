####### HELM Charts ###########

=> Using HELM chart we can install promethues server

=> Using HELM chart we can install grafana server

##################
Helm Installation
##################

```
 curl -fsSl -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3

 chmod 700 get_helm.sh

 ./get_helm.sh

 helm

```

-> check do we have metrics server on the cluster

```
kubectl top pods
```

```
kubectl top nodes
```

# check helm repos.

```
 helm repo ls
```

# Add the metrics-server repo to helm

```
helm repo add metrics-server https://kubernetes-sigs.github.io/metrics-server/
```

# Install the chart

```
 helm upgrade --install metrics-server metrics-server/metrics-server
```

#####Install Prometheus & Grafana In K8S Cluster using HELM#######

# Add the latest helm repository in Kubernetes

```
helm repo add stable https://charts.helm.sh/stable
```

# Add prometheus repo to helm

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```

# Update Helm Repo

```
helm repo update
```

# install prometheus

```
helm install stable prometheus-community/kube-prometheus-stack
```

# Get all pods

```
kubectl get pods
```

Note: You should see prometheus pods running

# Check the services

```

kubectl get svc

```

# By default prometheus and grafana services are available within the cluster as ClusterIP, to access them outside lets change it to LoadBalancer.

# Edit Prometheus Service & change service type to LoadBalancer then save and close that file

```

kubectl edit svc stable-kube-prometheus-sta-prometheus

```

# Now edit the grafana service & change service type to LoadBalancer then save and close that file

```

kubectl edit svc stable-grafana

```

# Verify the service if changed to LoadBalancer

```

kubectl get svc

```

# Access Promethues server using below URL

    URL : http://LBR-DNS:9090/

# Access Grafana server using below URL

    URL : http://LBR-DNS/

=> Use below credentials to login into grafana server

```

UserName: admin
Password: prom-operator

```

---

## => Once we login into Grafana then we can monitor our k8s cluster. Grafana will provide all the data in charts format.

---
