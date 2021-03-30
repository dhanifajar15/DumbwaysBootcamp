# VMware - Install Application

* #### Login ke Ubuntu Server pada VMware
![01](assets/Selection_343.png)
![01](assets/Selection_344.png)

* #### Remote server dari client denga SSH Server dan coba ping untuk cek koneksi 
![01](assets/Selection_346.png)

* #### Update Server menggunakan Command
    `sudo apt-get update`

![02](assets/Selection_347.png)

* #### Install Nginx Menggunakan Command dan coba cek nginx dengan curl localhost
    `sudo apt -y install nginx`

![03](assets/Selection_348.png)
* #### Tes Nginx pada browser dengan memasukkan IP server pada url
![04](assets/Selection_349.png)

* #### Install nvm Menggunakan Command
    ```
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
    ```

![05](assets/354.png)

* #### Cek versi nvm yang tersedia
![01](assets/Selection_355.png)
![01](assets/Selection_356.png)

* #### Install node dengan versi lts paling terbaru
![01](assets/Selection_357.png)

* #### Cek versi node dan nvm
![01](assets/Selection_359.png)

* #### Clone Repo Library dan Masuk Ke Direktori dengan menggunakan Command
    `git clone https://github.com/sgnd/wayshub-frontend`

![07](assets/Selection_360.png)

* #### Lakukan Install npm package dan deploy dengan Command
    ```
    npm install
    npm start
    ```

![08](assets/Selection_361.png)
![09](assets/Selection_365.png)
![09](assets/Selection_366.png)

* #### Buka Browser Masukkan Ip Adresses dengan port 3000

![10](assets/Selection_363.png)
