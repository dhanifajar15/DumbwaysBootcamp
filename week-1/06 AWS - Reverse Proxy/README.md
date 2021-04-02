# AWS - Reverse Proxy

## 1. Install Webserver Nginx di Reverse Proxy Server
Remote server reverse proxy dengan ssh 
![01](assets/Selection_444.png)

Update dan Upgrade OS di Reverse Proxy dengan Command
```
sudo apt update && sudo apt -y upgrade
```
![02](assets/Selection_437.png)

Kemudian Install Nginx dengan Command dan tes pada browser dengan menggunakan Public IPv4 address
```
sudo apt -y install nginx
```
![03](assets/Selection_438.png)

Kemudian Pindah Ke Direktori `/etc/nginx/` kemudian buat direktori baru `wayshub` dan buat file `frontend.conf`
![05](assets/Selection_439.png)

isi file `frontend.conf`
```
    server {
	listen 80;
	listen [::]:80;

	server_name 54.90.46.151;

	location / {
		proxy_pass http://10.0.100.99:3000;
	}
}
```
![06](assets/Selection_440.png)

Kemudian tambahkan folder `wayshub`  di `nginx.conf`
![07](assets/Selection_442.png)

Cek syntax untuk memastikan tidak ada kesalahan dengan
```
sudo nginx -t
```
![08](assets/Selection_441.png)

Restart Nginx dengan command
```
sudo systemctl restart nginx
```
![08](assets/Selection_443.png)

Tes akses dengan memasukkan IP lewat browser
![09](assets/Selection_445.png)
