* # AWS Setup Database

* ## Konfigurasi Database Server
### Install dan Konfigurasi MySQ di Server Database 1

#### Install paket `mysql-server` dan `mysql-client` dengan command:
```
sudo apt install mysql-server mysql-client
```
![02](assets/Selection_657.png)

####  Edit file /etc/mysql/mysql.conf.d/mysqld.cnf di database 1
```
server-id              = 1
log_bin                = /var/log/mysql/mysql-bin.log
binlog_do_db           = wayshub
#bind-address          = 127.0.0.1
```
![02](assets/Selection_658.png)

####  Sekarang restart service mysql:
```
sudo systemctl restart mysql.service
```
![02](assets/Selection_659.png)

####  Kemudian masuk ke mysql melalui terminal:
```
mysql -u root -p
```
![02](assets/Selection_660.png)

#### membuat pseudo-user yang nanti akan mereplikasi database antara 2 server
```
create user 'replicator'@'%' identified by 'dhani';
```
![02](assets/Selection_661.png)

####  Buat juga database yang akan di replikasi.
```
create database wayshub;
```
![02](assets/Selection_662.png)

####  Kemudian berikan permission ke user agar bisa mereplikasi database:
```
grant replication slave on *.* to 'replicator'@'%';
```
![02](assets/Selection_663.png)

####  mengetahui informasi mengenai status master mysql yang nanti akan dibutuhkan untuk konfigurasi Database 2
```
show master status;
```
![02](assets/Selection_664.png)

### Install dan Konfigurasi MySQ di Server Database 2

####  Edit file /etc/mysql/mysql.conf.d/mysqld.cnf di database 1
```
server-id              = 2
log_bin                = /var/log/mysql/mysql-bin.log
binlog_do_db           = wayshub
#bind-address          = 127.0.0.1
```
![02](assets/Selection_665.png)


####  Kemudian masuk ke mysql melalui terminal:
```
mysql -u root -p
```
![02](assets/Selection_666.png)

#### membuat pseudo-user yang nanti akan mereplikasi database antara 2 server
```
create user 'replicator'@'%' identified by 'dhani';
```
![02](assets/Selection_667.png)

####  Buat juga database yang akan di replikasi.
```
create database wayshub;
```
![02](assets/Selection_668.png)

####  Kemudian berikan permission ke user agar bisa mereplikasi database:
```
grant replication slave on *.* to 'replicator'@'%';
```
![02](assets/Selection_669.png)

####  Mengaktifkan replikasi dari Server A ke Server B, sesuaikan dengan informasi yang ada di database 1
```
stop slave; 
CHANGE MASTER TO MASTER_HOST = '10.0.100.221', MASTER_USER = 'replicator', MASTER_PASSWORD = 'dhani', MASTER_LOG_FILE = 'mysql-bin.000001', MASTER_LOG_POS = 107; 
start slave; 
```
![02](assets/Selection_671.png)
![02](assets/Selection_672.png)
![02](assets/Selection_673.png)

####  mengetahui informasi mengenai status master mysql yang nanti akan dibutuhkan untuk konfigurasi Database 1
```
show master status;
```
![02](assets/Selection_674.png)

### Konfigurasi Slave Server di Database 1 Server

####  Mengaktifkan replikasi dari Server B ke Server A, sesuaikan drngan informasi yang ada di database 2
```
stop slave; 
CHANGE MASTER TO MASTER_HOST = '10.0.100.221', MASTER_USER = 'replicator', MASTER_PASSWORD = 'dhani', MASTER_LOG_FILE = 'mysql-bin.000001', MASTER_LOG_POS = 107; 
start slave; 
```
![02](assets/Selection_676.png)
![02](assets/Selection_677.png)
![02](assets/Selection_678.png)

 
