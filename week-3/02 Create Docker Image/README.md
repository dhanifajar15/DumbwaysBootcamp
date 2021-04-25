# Create Docker Image

* #### Buat file `Dockerfile` pada Frontend and Backend
Frontend
```
FROM node:14
WORKDIR /usr/app
COPY . .
RUN npm instaZll
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
![01](assets/Selection_688.png)
![02](assets/Selection_689.png)

* #### Build dengan command
```
docker build -t namaimage:tag .
```
![03](assets/Selection_690.png)


![03](assets/Selection_693.png)


* #### check pada `docker images`
![04](assets/Selection_691.png)



![04](assets/Selection_694.png)

* #### Kemudian Push
```
docker push dhanifajar15:wayshub-frontend
```
![03](assets/Selection_692.png)

```
docker push dhanifajar15:wayshub-backend
```

![03](assets/Selection_695.png)


