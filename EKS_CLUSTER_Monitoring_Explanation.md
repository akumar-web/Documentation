# Monitoring Kubernetes with kube-prometheus-stack

I used the Prometheus Community Helm repository, which contains all Prometheus-related Helm charts including the kube-prometheus-stack.

## Steps:

### Add the Prometheus Community repository:

1. `helm repo add prometheus-community https://prometheus-community.github.io/helm-charts`
2. `helm search repo prometheus-community`
3. `helm search repo prometheus-community/kube-prometheus-stack`

**Install version 45.7.1 of the Kube Prometheus Stack. Here's the installation command:**

`helm install prometheus prometheus-community/kube-prometheus-stack --version 45.7.1 --namespace monitoring --create-namespace`

This installation deploys four main components into your Kubernetes cluster:

1. Prometheus Operator: Automates the creation of your Prometheus instance and alert manager  
2. Node Exporter: Extracts infrastructure metrics  
3. Kube State Metrics: Collects Kubernetes platform metrics  
4. Grafana: Visualization tool for metric data  

**The kube-prometheus-stack comes pre-configured for infrastructure monitoring through two main exporters:**

1. Node Exporter: Scrapes system-level metrics from Kubernetes nodes (CPU, memory usage, disk utilization)  
2. Kube State Metrics: Collects metrics about Kubernetes objects health, configuration, and availability  

**To access the Prometheus UI, use port forwarding:**

`kubectl port-forward svc/prometheus-operated -n monitoring 9090:9090`

**For a more visual experience, access Grafana:**

`kubectl port-forward svc/prometheus-grafana -n monitoring 3000:80`
