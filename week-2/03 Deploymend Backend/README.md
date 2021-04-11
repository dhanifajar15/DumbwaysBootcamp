# Deployment Backend

#### Install nvm dengan Command
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
![07](assets/Selection_523.png)

#### Install nvm dengan versi lts paling latest

![08](assets/Selection_524.png)

#### Git clone ke repo dikrektori library backend dengan command
```
git clone git@github.com:sgnd/wayshub-backend.git
```

![01](assets/Selection_521.png)


#### Ubah isi file `/config/config.json` dan isi sesuai ip dari instance load balancer database
![04](assets/Selection_528.png)


#### Install packages `npm install` dan pm2 `sudo npm install -g pm2` dan buat file `ecosystem.config.js`
![03](assets/Selection_525.png)
![04](assets/Selection_526.png)

```

module.exports = {
        apps: [
          {
            name: 'wayshub-backend',
            script: 'npm',
            args: 'start'
           }
        ]
};
```

![04](assets/Selection_534.png)

#### Install packages untuk migrate database dengan command `npm install -g sequelize-cli` 

![04](assets/Selection_527.png)

#### Lakukan migrasi database dengan command `sequelize db:migrate all` dan `sequelize db:seed:all` jika gagal install `sudo npm install -g mysql2` terlebih dahulu

![04](assets/Selection_532.png)

#### Jalankan command `pm2 start ecosystem.config.js`

![04](assets/Selection_537.png)

## Pada Frontend Server

#### Edit file di server frontend pada /config/config.js dan ganti base url dengan ip backend server dan lakukan command 
```
pm2 restart ecosystem.config.js
```

![04](assets/Selection_538.png)

