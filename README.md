# Kubernetes içerisinde EFK stack ile log toplama.

# İlk olarak namespace ve elasticsearch kaynaklarını oluşturuyoruz.
kubectl create -f namespace.yaml
kubectl create -f elasticsearch_statefulset.yaml

## test
kubectl port-forward es-cluster-0 9200:9200 --namespace=kube-logging
curl http://localhost:9200/_cluster/state?pretty

kubectl create -f kibana.yaml

kubectl port-forward kibana-5645d8d5b9-2dds4 5601:5601 --namespace=kube-logging
http://localhost:5601

kubectl create -f fluentd.yaml


kubectl create -f counter.yaml

