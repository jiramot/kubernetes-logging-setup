# ELK
### Add helm repo
```
helm repo add elastic https://helm.elastic.co
helm repo update
```

### Install elastic
```
helm install elasticsearch elastic/elasticsearch -n elastic-system --create-namespace -f elasticsearch/values.yaml
```
```
wget https://raw.githubusercontent.com/elastic/helm-charts/master/elasticsearch/examples/minikube/values.yaml
```
### Install kibana
```
helm install kibana elastic/kibana -n elastic-system
```
### Install logstash
```
helm install logstash elastic/logstash -n elastic-system
```
### Install fluentd
```
helm repo add fluent https://fluent.github.io/helm-charts
helm repo update
helm install fluentd fluent/fluentd --create-namespace -n elastic-system --values fluentd/values.yaml
```

### Install fluent-bit
```
helm install fluent-bit fluent/fluent-bit --create-namespace -n loggin-system --values fluent-bit/values.yaml
helm uninstall fluent-bit -n loggin-system
```
    [FILTER]
        Name          nest
        Match         kube.*
        Operation     lift
        Nested_under  kubernetes
    [FILTER]
        Name          nest
        Match         kube.*
        Operation     lift
        Nested_under  labels
    [FILTER]
        Name    grep
        Match   kube.*
        Regex   annotations['enableLogging'] true
    [FILTER]
        Name    grep
        Match   kube.*
        Regex   $kubernetes['namespace_name'] default

customParsers: |
[PARSER]
Name    demo-parser
Format  regex
Regex   ^(?<number>[^ ]+): (?<message>.*)$
```



```