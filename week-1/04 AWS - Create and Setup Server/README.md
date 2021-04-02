# AWS - Create and Setup Server

## Pertama Buat Virtual Private Cloud (VPC)

* #### 1. Membuat VPC dan Konfigurasi Subnet
Create VPC dan ubah Name tag dan IPv4 CIDR Block
![01](assets/Selection_380.png)

Kemudian buat Public Subnet dan Private Subnet
![02](assets/Selection_381.png)
![03](assets/Selection_382.png)

* #### 2. Buat VPC baru 
Buat Internet Gateway untuk konek VPC ke internet
![04](assets/Selection_383.png)

Attach Internet Gateway ke VPC
![05](assets/Selection_384.png)

Pada Route Table, Ganti Nama Router Default menjadi Public Route
![06](assets/Selection_385.png)

Tambahkan route dengan target internet gateway
![07](assets/Selection_387.png)

Kemudian Buat Private Route
![07](assets/07.png)

Buat Key Pair sebagai security credentials ketika connect ke sebuah instance
![09](assets/Selection_388.png)

Kemudian pada Security Gateway, buat SG NAT Instance dengan membuka SSH, HTTP, HTTPS, dan All Trafic pada IP tertentu
![11](assets/Selection_389.png)


## Kedua Membuat Public Ubuntu Server dan Private Ubuntu Server

* #### 1. Membuat EC2 Instance untuk Public Server

Pilih Ubuntu Server 20.04 LTS (HVM), SSD Volume Type Lalu Klik Select
![14](assets/Selection_390.png)

Kemudian Pilih Next:Configuration Instance Detail dengan Auto-assign Public Ip disable dan Public Subnet
![15](assets/Selection_391.png)

Untuk Storage dibiarkan default yaitu 8 Gb Kemudian Klik add tags
![17](assets/Selection_392.png)

Untuk bagian Security Group, arahkan pada NAT SG yang tadi telah kita buat. Lalu Klik Review and Launch dan Klik Launch
![19](assets/Selection_394.png)

Keypair digunakan untuk SSH ke Server jika Belum membuat dibuat terlebih dahulu. Jika sudah klik launch Instances
![20](assets/20.png)
![21](assets/21.png)

Kemudian Buat Elastic IP untuk Public Server
![22](assets/Selection_396.png)

Kemudian Pilih Elasic yg baru dibuat dan klik Assosicate Elastic IP Address
![23](assets/Selection_397.png)

Stop Source/Destination Check pada Instance Reverse Proxy 
![25](assets/Selection_398.png)

Pada Route Table, edit private route dengan target instance reverse proxy yang telah kita buat
![25](assets/Selection_399.png)

Hasil akhir Route Table
![25](assets/Selection_400.png)
* #### 2. Membuat EC2 Instance untuk Private Server

Launch Instance dan Pilih Ubuntu Server 20.04 LTS (HVM), SSD Volume Type Lalu Klik Select
![14](assets/Selection_404.png)

Kemudian Pilih Next:Configuration Instance Detail dan arahkan Subnet ke Private Subnet karena Private Server dan Autoassign disable Lalu Klik add storage
![15](assets/Selection_405.png)

Untuk Storage dibiarkan default yaitu 8 Gb Kemudian Klik add tags
![17](assets/17.png)


Untuk bagian Security Group Isi Seperti pada Gambar. Lalu Klik Review and Launch dan Klik Launch
All Traffic dengan Source Anywhere
![28](assets/Selection_406.png)

Hasil Terakhir:
![29](assets/Selection_411.png)

* #### 3. SSH ke Public Server Menggunakan Terminal
Pilih Reverse Proxy dan salin IP
![30](assets/Selection_418.png)

Buka Terminal dan Pindah ke Direktori Terdapat keypair
![32](assets/Selection_420.png)

 `chmod 400 dhani.pem` untuk mengatur hak akses file
![33](assets/Selection_421.png)

Hasil Terakhir dapat SSH ke Server Public
![34](assets/Selection_401.png)

* #### 4. Membuat New User di Public Server dan SSH Menggunakan password
Cek Koneksi dengan curl ke google
![35](assets/Selection_402.png)

Setting ip tables dengan perintah berikut pada server reverse proxy yang digunakan sebagai nat instance
![35](assets/Selection_403.png)

Kemudian edit file `/etc/ssh/sshd_config` dan ubah PasswordAuthentication menjadi Yes
![37](assets/Selection_407.png)

Membuat User baru dengan Command
```
sudo adduser reverseproxy
```

Kemudian usermod User reverseproxy dengan command
```
sudo usermod -aG sudo reverseproxy
```
Kemudian Restart dan Exit sshd Menggunakan Command
```
sudo systemctl restart sshd
```

![36](assets/Selection_408.png)

Kemudian SSH kembali dengan command `ssh user@ip` yaitu:
```
ssh reverseproxy@54.90.46.151
```
![39](assets/Selection_410.png)

* #### 5. SSH Private Server dari Public Server

Copy key pair ke public server dengan perintah
```
scp dhani.pem reverseproxy@54.90.46.151:~ 
```
![43](assets/Selection_409.png)
Kemudian Sama dengan Langkah public Server Pilih Frontend Server dan Copy Private Ipv4 addresses
![43](assets/Selection_419.png)

Hasil Akhir:
![44](assets/Selection_412.png)

Cek Koneksi dengan ping ke google
`ping www.google.com`
![45](assets/Selection_413.png)

* #### 6. Membuat New User di Private Server dan SSH Menggunakan password

Membuat User baru dengan Command
```
sudo adduser frontend
```
![45](assets/Selection_414.png)

Kemudian usermod User frontend dengan Command bertujuan untuk user tidak perlu menggunakan command dengan sudo didepannya
```
sudo usermod -aG sudo frontend
```
![45.5](assets/Selection_415.png)

Kemudian edit file `/etc/ssh/sshd_config` dan ubah PasswordAuthentication menjadi Yes

Kemudian Restart dan Exit sshd Menggunakan Command
```
sudo systemctl restart sshd
```
![47](assets/Selection_416.png)

Kemudian SSH kembali dengan command `ssh user@ip` yaitu :
```
ssh frontend@10.0.100.99
```
![48](assets/Selection_417.png)