# Connect Multiple Server

* #### Install Node-Exporter pada semua target server (frontend,backend,database,reverseproxy,jenkins,monitoring)
```
docker run -d --net="host" --pid="host" -v "/:/host:ro,rslave" quay.io/prometheus/node-exporter --path.rootfs=/host
```
![01](assets/Selection_733.png)


* #### edit file `prometheus.yml` dan tambahkan ip target
![08](assets/Selection_746.png)

* #### Cek pada prometheus.dhanifajar.onlinecamp.id
![09](assets/Selection_749.png)

* #### tambahkan prometheus pada grafana
![10](assets/Selection_745.png)

* #### Setting dashboard frontend backend

Untuk Query
CPU Usage
```
100 - (avg by(instance)(irate(node_cpu_seconds_total{instance="10.0.1.249:9100",job="node_exporter",mode="idle"}[5m]))*100)
```
![10](assets/Selection_765.png)


![10](assets/Selection_766.png)
Memory Usage
```
(node_memory_MemTotal_bytes{instance="10.0.1.249:9100",job="node_exporter"} - (node_memory_MemFree_bytes{instance="10.0.1.249:9100",job="node_exporter"} +        
node_memory_Cached_bytes{instance="10.0.1.249:9100",job="node_exporter"} + node_memory_Buffers_bytes{instance="10.0.1.249:9100",job="node_exporter"} )) /   
node_memory_MemTotal_bytes{instance="10.0.1.249:9100",job="node_exporter"} * 100
```
![10](assets/Selection_767.png)


![10](assets/Selection_768.png)
