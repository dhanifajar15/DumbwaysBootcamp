# Create Jenkins Jobs

* #### Generate Token Github dengan cara masuk klik Settings > Developer Settings > Personal Access Tokens
![01](assets/01.png)

* #### Pilih workflow dan admin:repo_hook
![02](assets/02.png)

* #### Masuk Ke Credentials dan Tambahan Credential dengan Secret Text kemudian Masuk Configuration Jenkins
![03](assets/03.png)

* #### Install Plugin Publish Over SSH dan tambahan Server untuk server target buka port 22 dari Server jenkins dan tambahan ssh-keygen jenkins di server frontend dan backend dan atur timeout 0ms
![05](assets/05.png)
![06](assets/06.png)
![07](assets/07.png)

* #### Buat freestyle project
![04](assets/04.png)

* #### Isi Source Code Management git
![08](assets/08.png)

* #### Centang Build Triggers pada pilihan github hook trigger
![09](assets/09.png)

* #### Isi Build
![10](assets/10.png)
![15](assets/15.png)

* #### dan atur exec timeout 0
![11](assets/11.png)

* #### Install Plugin Discord Notifier. Kemudian pada Discord Buat channel. Klik Server Setting > Integrations > Buat Webhook dan Copy
![12](assets/12.png)

* #### Copy URL pada Post Build
![13](assets/13.png)

* #### Klik Build dan akan ada notifikasi dari discord
![14](assets/14.png)
![16](assets/16.png)

* #### Hasil Akhir Output:
![17](assets/17.png)