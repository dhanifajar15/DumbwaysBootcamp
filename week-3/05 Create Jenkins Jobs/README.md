# Create Jenkins Jobs

* #### Generate Token Github dengan cara masuk klik Settings > Developer Settings > Personal Access Tokens dan Pilih workflow dan admin:repo_hook
![01](assets/Selection_709.png)


* #### Masuk Ke Credentials dan Tambahan Credential dengan Secret Text kemudian Masuk Configuration Jenkins
![03](assets/Selection_710.png)


![06](assets/Selection_711.png)

* #### Install Plugin Publish Over SSH dan tambahan Server untuk server target buka port 22 dari Server jenkins dan tambahan ssh-keygen jenkins di server frontend dan backend dan atur timeout 0ms
![05](assets/Selection_712.png)



![07](assets/Selection_713.png)



![07](assets/Selection_714.png)


![07](assets/Selection_715.png)


![07](assets/Selection_716.png)


![07](assets/Selection_717.png)


* #### Buat freestyle project dan Isi Source Code Management git
![08](assets/Selection_722.png)



* #### Centang Build Triggers pada pilihan github hook trigger
![09](assets/Selection_720.png)

* #### Isi Build
![10](assets/Selection_721.png)



![15](assets/Selection_723.png)

* #### dan atur exec timeout 0
![11](assets/11.png)

* #### Install Plugin Discord Notifier. Kemudian pada Discord Buat channel. Klik Server Setting > Integrations > Buat Webhook dan Copy
![12](assets/Selection_724.png)

* #### Copy URL pada Post Build
![13](assets/Selection_726.png)


* #### Hasil Akhir Output:
![17](assets/Selection_725.png)