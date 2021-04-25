# Setup Monitoring Server

* #### Buat user prometheus dan direktori kebutuhan prometheus dengan command
```
sudo useradd -rs /bin/false prometheus
sudo mkdir /etc/prometheus
sudo mkdir -p /data/prometheus
```
![03](assets/Selection_728.png)



![03](assets/Selection_730.png)

* #### Buat file `prometheus.yml`
```
cd /etc/prometheus/
sudo touch prometheus.yml
```
![04](assets/Selection_729.png)

* #### Ubah permissions dengan command
```
sudo chown prometheus:prometheus /data/prometheus /etc/prometheus/*
```
![05](assets/Selection_731.png)

* #### Isi file `prometheus.yml`
```
global:
  scrape_interval: 5s
scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['10.0.100.195:9090']
```
![06](assets/Selection_727.png)

* #### Jalankan Prometheus di docker dengan command
```
docker run -p 9090:9090 -d -v /etc/prometheus:/etc/prometheus prom/prometheus
```
![08](assets/Selection_735.png)

* #### Install Node-Exporter di docker dengan command
```
docker run -d --net="host" --pid="host" -v "/:/host:ro,rslave" quay.io/prometheus/node-exporter --path.rootfs=/host
```
![09](assets/Selection_733.png)

* #### Edit file `prometheus.yml` dan tambahkan node exporter
![10](assets/Selection_746.png)

* #### cek pada prometheus
![11](assets/Selection_738.png)

* #### Install Grafana di docker dengan command
```
docker run -d -p 3000:3000 --net=host grafana/grafana
```
![12](assets/Selection_742.png)

* #### Tambahkan Config pada Reverse Proxy dan lakukan configure SSL dengan command `sudo certbot --nginx -d monitoring.dhanifajar.onlinecamp.id` dan `sudo certbot --nginx -d prometheus.dhanifajar.onlinecamp.id`
```
server {
        listen 80;
        listen [::]:80;

        server_name monitoring.dhanifajar.onlinecamp.id;

        location / {
                proxy_pass http://10.0.100.195:3000;
        }
} 
```

```
server {
        listen 80;
        listen [::]:80;

        server_name prometheus.dhanifajar.onlinecamp.id;

        location / {
                proxy_pass http://10.0.100.195:9090;
        }
} 
```

![13](assets/Selection_740.png)




![14](assets/Selection_747.png) 
 

![15](assets/Selection_741.png)



![16](assets/Selection_748.png)

* #### Masuk ke `monitoring.dhanifajar.onlinecamp.id` login ke grafana default login admin pass admin
![17](assets/Selection_743.png)