Docker 部署开源监控系统Prometheus

环境：需要docker

```
docker pull prom/node-exporter
docker pull prom/prometheus
docker pull grafana/grafana
```

启动node-exporter

```
docker run -d -p 9100:9100 \
  -v "/proc:/host/proc:ro" \
  -v "/sys:/host/sys:ro" \
  -v "/:/rootfs:ro" \
  --net="host" \
  prom/node-exporter
```



新建目录Prometheus，编辑配置文件

```
mkdir /opt/prometheus
cd /opt/prometheus/
vim prometheus.yml
```

```
global:
  scrape_interval:     60s
  evaluation_interval: 60s
 
scrape_configs:
  - job_name: prometheus
    static_configs:
      - targets: ['localhost:9090']
        labels:
          instance: prometheus
 
  - job_name: linux
    static_configs:
      - targets: ['192.168.91.132:9100']
        labels:
          instance: localhost
```

```
docker run  -d \
  -p 9090:9090 \
  -v /opt/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml  \
  prom/prometheus
```

