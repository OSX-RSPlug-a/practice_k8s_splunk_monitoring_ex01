# practice_k8s_splunk_monitoring_ex01
K8S cluster with Splunk monitoring

Running the cluster:

      kubectl apply k8s/deployment.yaml

Installing Splunk by helm:

      helm repo add splunk-otel-collector-chart https://signalfx.github.io/splunk-otel-collector-chart

      helm install my-splunk-otel-collector --set="splunkPlatform.endpoint=https://127.0.0.1:8088/services/collector,splunkPlatform.token=xxxxxx,splunkPlatform.metricsIndex=k8s-metrics,splunkPlatform.index=main,clusterName=my-cluster" splunk-otel-collector-chart/splunk-otel-collector


Add these lines in the deployment-prometheus file:

                  autodetect:
                     prometheus: true
                  metadata:
                     annotations:
                        prometheus.io/scrape: "true"
                        prometheus.io/path: /metrics
                        prometheus.io/port: "8080"


And then execute this command:

      helm -n otel install my-splunk-otel-collector -f values.yaml splunk-otel-collector-chart/splunk-otel-collector
