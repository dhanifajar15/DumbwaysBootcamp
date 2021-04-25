# Create Docker Image

* #### Buat file `Dockerfile` pada Frontend and Backend
Frontend
```
FROM node:14
WORKDIR /usr/app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm","start"] 
```
Backend
```
FROM node:14
WORKDIR /usr/app
COPY . .
RUN npm install
EXPOSE 5000
CMD ["npm","start"] 
```
![01](assets/01.png)
![02](assets/02.png)

* #### Build dengan command
```
docker build -t namaimage:tag .
```
![03](assets/03.png)


* #### check pada `docker images`
![04](assets/04.png)

* #### Kemudian Push
```
docker push dhanifajar15:wayshub-frontend
```
![05](assets/05.png)
```
docker push dhanifajar15:wayshub-backend
```
