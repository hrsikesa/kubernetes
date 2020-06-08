This is Repo contains manifests  for  deploying  EFK(ElasticSearch, FluentD, Kibana) Stack on Kubernetes.

We run ElastiSearch as StatefulSets, Kibana as Deployment, FluentD as DaemonSets


Create a Namespace kube-logging, We will deploy EFK Stack in this Namespace.

In Stateful Set we are running 3 Replicas, but we can decrease or increasing it as per our requirenment
Also we will be using Headless Service for accessing ElasticSearch Pods.
Service Name/DNS of Accessing Particular Pod - es-cluster-0.elasticsearch.kube-logging.svc.cluster.local
where es-cluster-0 = Name of Pod, elasticsearch.kube=ServiceName   kube-logging=Namespace
We use it so we can access particular Pod, instead of to just accesing Service.

FluentD - DaemonSet will run on all Nodes.
We are not creating Service for FluentD Pods as they will only send logs to ElasticSearch
