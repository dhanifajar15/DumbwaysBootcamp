* # AWS Setup Database

* ## Konfigurasi Database Server
* #### SSH ke Database Server
![02](assets/01.png)

* #### install mysql di database server menggunakan command dan pilih versi 5.7
`wget https://dev.mysql.com/get/mysql-apt-config_0.8.15-1_all.deb`
![02](assets/02.png)

`sudo dpkg -i mysql-apt-config_0.8.15-1_all.deb`
![03](assets/03.png)
![04](assets/04.png)

`sudo apt update && sudo apt -y upgrade`
![05](assets/05.png)

`sudo apt -y install mysql-server` dan isikan password
![06](assets/06.png)
![07](assets/07.png)

* #### Buat user baru dan inisialisasi dengan 2 backend server

```
mysql -u root -p

CREATE USER 'backend'@'10.0.1.126' IDENTIFIED BY 'anjar'; 

GRANT ALL PRIVILEGES ON *.* TO 'backend'@'10.0.1.126';

FLUSH PRIVILEGES;
```
catatan `'user'@'ip-backend' Identified By 'password';`

![08](assets/08.png)
![09](assets/09.png)

* #### bind ip adress backend dengan database dan ubah ip bind adress menjadi ip Database Server
`sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf` 
![10](assets/10.png)

* #### restart mysql
![11](assets/11.png)

* ## Konfigurasi Backend Server
* #### SSH ke server backend dan install mysql-client dengan command
```
sudo apt-get update

sudo apt-get install -y mysql-client
```
![12](assets/12.png)

* #### akses database server dari backend server menggunakan command
`mysql -u backend -h 10.0.1.58 -p`
![13](assets/13.png)

* ## Konfigurasi Master-Slave Replication Database 

* #### Ubah file `mysqld.cnf` dengan tambahan server id=1 untuk master dan log_bin dan restart mysql (database1)
`sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf` 
![14](assets/14.png)

* #### buat replikasi user (database1)
```
mysql -u root
CREATE USER 'repl'@'%' IDENTIFIED BY 'slavepassword';
GRANT REPLICATION SLAVE ON *.* TO 'repl'@'%';
exit
```
![15](assets/15.png)

* #### buat snapshot dan copy ke server slave atau database2
```
mysqldump -u root -p --all-databases --master-data > masterdump.sql
scp masterdump.sql database02@10.0.1.176:
```
![16](assets/16.png)

* #### Ubah file `mysqld.cnf` dengan tambahan server id=2 dan bind adress diganti ip private (database2) dan restart mysql
`sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`
![17](assets/17.png)

* #### setting slave database untuk ke host master database
```
mysql -u root
CHANGE MASTER TO
MASTER_HOST='10.0.1.237',
MASTER_USER='repl',
MASTER_PASSWORD='slavepassword';
exit
```
![18](assets/18.png)

* #### Restore the snapshot pada slave database (database2)
`mysql -uroot -p < masterdump.sql`
![19](assets/19.png)

* #### Check status slave database
![20](assets/20.png)

* #### tes sinkronisasi
![21](assets/21.png)
![22](assets/22.png)