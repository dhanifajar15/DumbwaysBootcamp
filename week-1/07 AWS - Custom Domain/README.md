# AWS - Custom Domain

Tambahkan Subdomain DNS di Cloudfare
![03](assets/Selection_446.png)

Buat direktori `.secrets` di home user
![02](assets/Selection_447.png)

Masuk ke direktori `.secrets` dan buat file dengan nama `cloudflare.ini`
![02](assets/Selection_448.png)

Masukkan email dan api key yang telah terdaftar di cloudflare
![02](assets/Selection_449.png)

Ubah hak akses direktori `.secrets`
![02](assets/Selection_450.png)

Ubah hak akses file `cloudflare.ini`
![02](assets/Selection_452.png)

Ubah hak ases direktori `.secrets`
![02](assets/Selection_450.png)

Install certbot dengan perintah`sudo snap install --classic certbot`
![02](assets/Selection_453.png)

Install CloudFlare DNS authenticator plugin
![02](assets/Selection_454.png)

Jalankan certbot dengan Cloudflare authenticator dengan command`sudo certbot certonly --dns-cloudflare --dns-cloudflare-credentials /root/.secrets/cloudflare.ini -d dhani.online.camp.id --preferred-challenges dns-01`
![02](assets/Selection_455.png)

Ubah proxy status menjadi DNS only
![02](assets/Selection_456.png)

Ubah file `etc/nginx/wayshub/frontend.conf` bagian server name menjadi DNS `dhani.onlinecamp.id`
![01](assets/Selection_457.png)

Restart nginx dan masukkan Subdomain di Browser
![02](assets/Selection_459.png)