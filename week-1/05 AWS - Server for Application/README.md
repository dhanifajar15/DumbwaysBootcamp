# AWS - Server for Application

#### 1. Deploy Aplikasi Wayshub di Server Frontend 
SSH ke Server Frontend Melalui Public Server
![05](assets/Selection_422.png)

Update dan Upgrade OS dengan Command
```
sudo apt update && sudo apt -y upgrade
```  
![06](assets/Selection_423.png)

Kemudian Install nvm dengan Command
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
![07](assets/Selection_424.png)

Pastikan nvm sudah terinstall dengan memverifikasinya
![08](assets/Selection_425.png)

Cek available versi node
![08](assets/Selection_426.png)
![08](assets/Selection_427.png)

Install nvm dengan versi lts paling latest
![08](assets/Selection_428.png)

Melihat nvm yang sudah terinstall
![08](assets/Selection_429.png)

Cek versi node dan npm
![08](assets/Selection_430.png)

Clone Repo Library dan Masuk Ke Direktori dengan menggunakan Command
```
git clone https://github.com/sgnd/wayshub-frontend.git
```
![08](assets/Selection_432.png)

Kemudian install module dengan command
```
npm install
```
![11](assets/Selection_431.png)

Kemudian Install npm pm2 dengan command
```
sudo npm install -g pm2
```
![11](assets/Selection_431.png)

Kemudian generate file ecosystem.config.js dengan command 
```
pm2 ecosystem
```
![11](assets/Selection_433.png)

Edit file ecosystem.config.js
![11](assets/Selection_434.png)

Kemudian Jalankan pm2 dengan command 
```
pm2 start ecosystem.config.js
```
![12](assets/Selection_436.png)

