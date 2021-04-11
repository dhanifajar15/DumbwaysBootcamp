* # AWS Setup Database

* ## Konfigurasi Database Server
### Install dan Konfigurasi MySQ di Server Database 1 
![02](assets/01.png)

#### Install paket `mysql-server` dan `mysql-client` dengan command:
```
sudo apt install mysql-server mysql-client
```
![02](assets/02.png)

####  Edit file /etc/mysql/mysql.conf.d/mysqld.cnf di database 1
```
server-id              = 1
log_bin                = /var/log/mysql/mysql-bin.log
binlog_do_db           = wayshub
#bind-address          = 127.0.0.1
```
![02](assets/02.png)

####  Sekarang restart service mysql:
```
sudo systemctl restart mysql.service
```
![02](assets/02.png)

####  Kemudian masuk ke mysql melalui terminal:
```
mysql -u root -p
```
![02](assets/02.png)

#### membuat pseudo-user yang nanti akan mereplikasi database antara 2 server
```
create user 'replicator'@'%' identified by 'dhani';
```
![02](assets/02.png)

####  Buat juga database yang akan di replikasi.
```
create database wayshub;
```
![02](assets/02.png)

####  Kemudian berikan permission ke user agar bisa mereplikasi database:
```
grant replication slave on *.* to 'replicator'@'%';
```
![02](assets/02.png)

####  mengetahui informasi mengenai status master mysql yang nanti akan dibutuhkan untuk konfigurasi Database 2
```
show master status;
```
![02](assets/02.png)

### Install dan Konfigurasi MySQ di Server Database 2

#### Install paket `mysql-server` dan `mysql-client` dengan command:
```
sudo apt install mysql-server mysql-client
```
![02](assets/02.png)

####  Edit file /etc/mysql/mysql.conf.d/mysqld.cnf di database 1
```
server-id              = 2
log_bin                = /var/log/mysql/mysql-bin.log
binlog_do_db           = wayshub
#bind-address          = 127.0.0.1
```
![02](assets/02.png)

####  Sekarang restart service mysql:
```
sudo systemctl restart mysql.service
```
![02](assets/02.png)

####  Kemudian masuk ke mysql melalui terminal:
```
mysql -u root -p
```
![02](assets/02.png)

#### membuat pseudo-user yang nanti akan mereplikasi database antara 2 server
```
create user 'replicator'@'%' identified by 'dhani';
```
![02](assets/02.png)

####  Buat juga database yang akan di replikasi.
```
create database wayshub;
```
![02](assets/02.png)

####  Kemudian berikan permission ke user agar bisa mereplikasi database:
```
grant replication slave on *.* to 'replicator'@'%';
```
![02](assets/02.png)

####  Mengaktifkan replikasi dari Server A ke Server B, sesuaikan dengan informasi yang ada di database 1
```
stop slave; 
CHANGE MASTER TO MASTER_HOST = '10.0.100.221', MASTER_USER = 'replicator', MASTER_PASSWORD = 'dhani', MASTER_LOG_FILE = 'mysql-bin.000001', MASTER_LOG_POS = 107; 
start slave; 
```
![02](assets/02.png)

####  mengetahui informasi mengenai status master mysql yang nanti akan dibutuhkan untuk konfigurasi Database 1
```
show master status;
```
![02](assets/02.png)

### Konfigurasi Slave Server di Database 1 Server

####  Mengaktifkan replikasi dari Server B ke Server A, sesuaikan drngan informasi yang ada di database 2
```
stop slave; 
CHANGE MASTER TO MASTER_HOST = '10.0.100.221', MASTER_USER = 'replicator', MASTER_PASSWORD = 'dhani', MASTER_LOG_FILE = 'mysql-bin.000001', MASTER_LOG_POS = 107; 
start slave; 
```
![02](assets/02.png)

* ## Load Balance MySQL dengan Haproxy
#### Pertama kita harus membuat 2 user di MySQL server yang nantinya akan digunakan oleh si HAProxy. User pertama akan digunakan si HAProxy untuk mengecek status dari si server.
```
root@database# mysql -u root -p -e "INSERT INTO mysql.user (Host,User) values ('172.19.0.254','haproxy_check'); FLUSH PRIVILEGES;"
```

![02](assets/01.png)

#### User yang kedua harus memilki privileges setara dengan root yang nanti digunakan si HAProxy untuk mengakses server
```
mysql -u root -p -e "GRANT ALL PRIVILEGES ON *.* TO 'haproxy_root'@'172.19.0.254' IDENTIFIED BY 'dhani' WITH GRANT OPTION; FLUSH PRIVILEGES"
```

![02](assets/01.png)

####   Menginstall MySql client di Load Balancer
```
apt-get install mysql-client
```
![02](assets/02.png)

####  Tes untuk melihat database yang ada di Master dengan menggunakan user haproxy_root.
```
mysql -h 172.19.0.1 -u haproxy_root -p -e "SHOW DATABASES"
```
![02](assets/02.png)

####  Install paket haproxy di server Load Balancer
```
apt-get install haproxy
```
![02](assets/02.png)

####  Enable HAProxy
```
sed -i "s/ENABLED=0/ENABLED=1/" /etc/default/haproxy
```
![02](assets/02.png)

####  Backup file /etc/haproxy/haproxy.cfg
```
cp /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.cfg.bak
```
![02](assets/02.png)

####   Edit file tersebut
```
nano /etc/haproxy/haproxy.cfg
```
![02](assets/02.png)

####  Tambahkan baris berikut
```
global
    log 127.0.0.1 local0 notice
    user haproxy
    group haproxy

defaults
    log global
    retries 2
    timeout connect 3000
    timeout server 5000
    timeout client 5000

listen mysql-cluster
    bind 0.0.0.0:3306
    mode tcp
    option mysql-check user haproxy_check
    balance roundrobin
    server mysql-1 172.19.0.1:3306 check
    server mysql-2 172.19.0.2:3306 check weight 2
```
![02](assets/02.png)

####  Sekarang tinggal jalankan service dari HAProxy
```
service haproxy start
```
![02](assets/02.png)

#### Tes untuk menampilkan database di HAProxy
```
mysql -h 127.0.0.1 -u haproxy_root -p -e "SHOW DATABASES"
```
![02](assets/02.png)

####  Testing Load Balancing dengan menjalankan query menjalankan query dua kali.
```
mysql -h 127.0.0.1 -u haproxy_root -p -e "show variables like 'server_id'"
```
![02](assets/02.png)

