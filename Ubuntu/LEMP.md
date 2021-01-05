# Server Web Nginx
## 1.Pertama Menginstal Server Web Nginx
```
sudo apt update
sudo apt install nginx
```
## Open Firewall
Untuk melihat list yang dapat dibuka
```
sudo ufw app list
```
tambahan allow rule
```
sudo ufw allow 'Nginx HTTP'
```
untuk melihat perubahan
```
sudo ufw status
```
Jika Anda tidak memiliki nama domain yang mengarah ke server Anda dan Anda tidak mengetahui alamat IP publik server Anda, Anda dapat menemukannya dengan menjalankan perintah berikut:
```
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
```
# Secure HTTP on Nginx With Let's encrypt
Tambahan repository pada ubuntu
```
sudo add-apt-repository ppa:certbot/certbot
```
