# Install Application

* ## Menggunakan Docker Compose
* #### buat file `docker-compose.yml` dan isi file
Frontend
```
version: '3.8'
services:
  library-frontend:
     container_name: libraryfe
     image: anjardanis/libraryfe
     stdin_open: true
     ports:
       - 3000:3000

```
Backend
```
version: '3.8'
services:
  library-backend:
     container_name: librarybe
     image: anjardanis/librarybe
     stdin_open: true
     ports:
       - 5000:5000

```
![01](assets/01.png)
![02](assets/02.png)

![03](assets/03.png)
![04](assets/04.png)