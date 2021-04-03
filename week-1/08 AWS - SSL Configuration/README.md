# AWS - SSL Configuration

Ubah proxy status menjadi `Proxied`
![01](assets/Selection_460.png)

Aktivasi HTTPS dengan command
```
sudo certbot
```
![02](assets/Selection_461.png)
![01](assets/Selection_462.png)

Cek apakah HTTPS sudah ter-regenerate di file frontend.conf pada `/etc/nginx/wayshub/frontend.conf` 
![01](assets/Selection_463.png)

Reload nginx setelah melakukan perubahan  dengan command
```
sudo systemctl reload nginx
```
![01](assets/Selection_464.png)

Tes akses ke browser dengan memasukkan domain dan cek certificate
```
https://dhani.onlinecamp.id
```
![06](assets/Selection_466.png)