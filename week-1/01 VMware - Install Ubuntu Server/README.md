# VMware - Install Ubuntu Server


* #### Isi Nama File dan Pilih Ubuntu 64 Bit
![02](assets/Selection_317.png)

* #### Pilih Memory 1 Gb karena hanya untuk keperluan server
![03](assets/Selection_318.png)

* #### Create Virtual Hard disk
![04](assets/Selection_319.png)

* #### Pilih VDI ( VirtualBox Disk Image)
![05](assets/Selection_320.png)

* #### Pilih Dynamic Allocate
![06](assets/Selection_321.png)

* #### Pilih Size 8 GB
![07](assets/Selection_322.png)

* #### Cek interface yang sedang terkoneksi ke internet, disini saya memakai wireless lan (wlp3s0)
![09](assets/Selection_325.png)

* #### Klik Setting Ubah Network menjadi Bridge
![09](assets/Selection_324.png)

* #### Klik Storage Pilih ISO Ubuntu 18.04
![10](assets/Selection_323.png)


* #### Lalu Klik Start
![12](assets/Selection_326.png)

* #### Lalu Pilih Bahasa Inggris dan Continue Without Updating
![17](assets/Selection_327.png)
![18](assets/Selection_328.png)

* #### Lalu Klik Done Pada Pengaturan 
![19](assets/Selection_329.png)
* #### Cek IP laptop pada interface wlp3s0 untuk membuat ip static
![20](assets/Selection_330.png)
* #### Cek Gateway 
![21](assets/Selection_331.png)
* #### Edit network connection dengan settingan IPv4 manual
![22](assets/Selection_332.png)
![22](assets/Selection_333.png)

* #### Done saja pada Configure Proxy dan Ubuntu Mirror
![21](assets/Selection_334.png)

* #### Pilih Adding GPT Partition 1 GB Untuk Format Swap dan Sisanya Untuk Format Ext4
![A](assets/Selection_336.png)
![24](assets/Selection_337.png)


* #### Kemudian Done dan Pilih Continue
![25](assets/Selection_338.png)

* #### Isi Profile
![28](assets/Selection_339.png)

* #### Pilih Ceklis atau X untuk Install OpenSSH Server
![29](assets/Selection_340.png)

* #### Klik Done saja pada Featured Server Snaps
![28](assets/Selection_341.png)

* #### Kemudian Pilih Done dan Menunggu Install dan Reboot Server
![30](assets/Selection_342.png)