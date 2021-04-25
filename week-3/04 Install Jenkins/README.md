# Install Jenkins

* #### Menginstall jenkins dari docker dengan command
```
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/usr/app jenkins/jenkins:lts
```
![01](assets/Selection_701.png)

* #### Cek container jenkins untuk memastikan berjalan
```
docker ps
```
![02](assets/Selection_702.png)

* #### Dapatkan initial password dengan command
```
docker exec -it ${CONTAINER_ID or CONTAINER_NAME} 
cat /var/jenkins_home/secrets/initialAdminPassword
```
![02](assets/Selection_703.png)

* #### buka `cicd.dhanifajar.onlinecamp.id` dan masukkan inital password
![03](assets/Selection_704.png)

* #### ikuti petunjuk daftar mengisi username dan instalasi jenkins
![04](assets/Selection_708.png)


* #### Pilih plugin yang direkomendasikan
![05](assets/Selection_705.png)


![05](assets/Selection_707.png)
