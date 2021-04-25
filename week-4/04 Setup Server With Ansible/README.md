# Setup Server Ansible

* #### Install Ansible pada Monitoring Server dengan command
```
sudo apt -y update && sudo apt -y upgrade
sudo apt-get -y install python3
sudo apt install whois -y
sudo apt-add-repository ppa:ansible/ansible
sudo apt -y install ansible
```
![01](assets/01.png)

* #### Buat Direktori Baru `Ansible` dan tambahkan file `ansible.cfg`
![02](assets/02.png)

* #### Buat file `Inventory` yang berisi host semua server dan buat direktori `ssh` yang berisi key
![03](assets/03.png)

* #### tes ping dikarenakan nginx masih user ubuntu jadi dipisah antara non user dan user
![04](assets/04.png)
![05](assets/05.png)

* #### Buat instance frontend baru dan tambahkan di Inventory
![06](assets/06.png)

* #### lakukan update dan upgrade pada instance frontend baru dengan command
```
ansible new -m apt -a update_cache=true --become
ansible new -m apt -a "upgrade=dist" --become
```
![07](assets/07.png)

* #### Selanjutnya buat user frontend02 pertama buat password terenkripsi dengan command
```
mkpasswd --method=SHA-512
```
$6$CjI1u8z2chKyEka$ka/CR75ySm.Dchny13kVH6UTFu1jJZsUM9HZnCAQWkiJIgEcgDSjgxGA97Wai5P76AxGf9C9s/O.N/vr2r7gm0
![08](assets/08.png)

* #### buat file yaml `create_user.yml` dan masukkan password yang terenkripsi
![09](assets/09.png)

* #### jalan ansible playbook
![10](assets/10.png)

* #### selanjutnya install docker dan node exporter docker ganti user fe2 di Inventory
![11](assets/11.png)
![12](assets/12.png)

* #### buat ssh key untuk git repository
![13](assets/13.png)
![14](assets/14.png)

* #### git repository library-fe
![15](assets/15.png)
![16](assets/16.png)

* #### lakukan docker build di frontend02 dan run dari ansible
![17](assets/17.png)
![18](assets/18.png)
![19](assets/19.png)