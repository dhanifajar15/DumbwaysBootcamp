# Install Jenkins

* #### Menginstall jenkins dari docker dengan command
```
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/usr/app jenkins/jenkins:lts
```
![01](assets/01.png)

* #### Dapatkan initial password dengan command
```
docker exec -it ${CONTAINER_ID or CONTAINER_NAME} cat /var/jenkins_home/secrets/initialAdminPassword
```
![02](assets/02.png)

* #### buka `cicd.anjar.instructype.com` dan masukkan inital password
![03](assets/03.png)

* #### ikuti petunjuk daftar mengisi username dan instalasi jenkins
![04](assets/04.png)


* ## Pindah pada Reverse Proxy buat file jenkins.conf pada /etc/nginx reverse proxy
![05](assets/05.png)

* #### Buat file jenkins.conf dan lakukan SSL configuration
`sudo certbot --nginx -d cicd.anjar.instructype.com`
![06](assets/06.png)