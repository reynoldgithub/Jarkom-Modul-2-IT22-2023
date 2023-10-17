# LAPORAN RESMI MODUL 3 JARKOM
# IT 22
-   Reynold Putra Merdeka | 5027211034
-   Rakha Aldo Nirwasita  | 5027211054



Pada modul 3 ini kami diberikan 1-20 soal cerita yang bersambung untuk diselesaikan, dan berikut dokumentasi dan catatan mengenai pengerjaan dan penyelesaiannya

## Soal 1
Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. _pada modul ini kami diberikan topologi no 2_

### NOTE:
<br>

**Client:** 
<br>
Sadewa & Nakula

**DNS Master:**
<br>
Yudhistira
<br>

**DNS Slave (Werkudara Load Balancer):** 
<br>
Arjuna
<br>

**Web Server:**
<br>
Prabukusuma, Abimanyu, Wisanggeni

<br> 

![02](https://github.com/reynoldgithub/Jarkom-Modul-2-IT22-2023/assets/103549279/5ebb9a69-b7aa-4273-8a72-3858c531eb5a)
Topologi No.2

<br>

![image](https://github.com/reynoldgithub/Jarkom-Modul-2-IT22-2023/assets/103549279/f1a83bc9-4bb5-4441-b375-b28def96edb0)
Hasil dari kelompok kami


## Soal 2
Buatlah website utama pada node arjuna dengan akses ke ```arjuna.yyy.com``` dengan alias ```www.arjuna.yyy.com``` dengan **yyy** merupakan kode kelompok (_www.arjuna.it22.com_).

### Yudhistira
pada yudhistira melakukan konfigurasi di ```/etc/bind/named.conf.local``` yang berisikan:

```
zone “arjuna.it03.com” {
	type master;
	file “/etc/bind/jarkom/arjuna.it03.com
};
```
kemudian membuat folder **jarkom** dan kemudian dengan command ```nano/etc/bind/arjuna.it22.com``` di terminal untuk membuat file **arjuna.it22.com**.


<img width="522" alt="image" src="https://github.com/reynoldgithub/Jarkom-Modul-2-IT22-2023/assets/103549279/0f1a87f9-e885-4e92-b48f-fc04f6b1761f">

lalu melakukan restart pada bind9 ```service bind9 restart```

### Sadewa
pada **sadewa** melakukan konfigurasi pada ```/etc/resolv.conf``` dengan mengganti ip yang  sesuai yakni ```192.244``` 
<img width="524" alt="image" src="https://github.com/reynoldgithub/Jarkom-Modul-2-IT22-2023/assets/103549279/51797e5d-78a7-425a-b38f-b449c9c65a3c">

kemudian lakukan ```ping arjuna.it22.com``` 

<img width="394" alt="image" src="https://github.com/reynoldgithub/Jarkom-Modul-2-IT22-2023/assets/103549279/f9753339-9813-4431-bebf-08624f604a2a">

akan memberikan ping sedimikian 

## Soal 3
Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.

## Soal 4
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.

## Soal 5
Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)

## Soal 6
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.

## Soal 7
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.

## Soal 8
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.


## Soal 9
Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.


## Soal 10
Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. 

- Prabakusuma:8001
- Abimanyu:8002
- Wisanggeni:8003

pertama-tama akan dilakukan konfigurasi pada ```/etc/nginx/sites-available/lb```

### /etc/nginx/sites-available/lb
<img width="279" alt="image" src="https://github.com/reynoldgithub/Jarkom-Modul-2-IT22-2023/assets/103549279/32aca7d8-6502-4395-91d1-cded1fdb5955">

kemudian melakukan konfigurasi pada nginx yakni ```/etc/nginx/nginx.conf```

### /etc/nginx/nginx
setelah itu lakukan command ```service nginx restart``` untuk merestart nginx


## Nomer 11
> Selain menggunakan Nginx, lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server www.abimanyu.yyy.com. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.yyy
- Install deps
```bash
apt-get install wget unzip apache2 libapache2-mod-php7.0 -y
```
- Download file then unzip

```bash
wget -O /root/abimanyu.zip "https://drive.usercontent.google.com/download?id=17tAM_XDKYWDvF-JJix1x7txvTBEax7vX&export=download&authuser=0&confirm=t&uuid=e1ee8117-918e-4a79-880c-7e7f9f14767a&at=APZUnTUybl6ig4kiWHRb7ghy3N0p:1697383050378"

uznip /root/abimanyu.zip
```
- Copy file to /var/www
```bash
cp -r /root/abimanyu.yyy.com /var/www/abimanyu.it22
```
- Create apache config
```bash
# /etc/apache2/site-available/abaimanyu.it22.com
<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/abimanyu.it22
        ServerName abimanyu.it22.com
        ServerAlias www.abimanyu.it22.com
        ServerAlias 192.244.2.6

        Alias "/home" "/var/www/abimanyu.it22/home.html"

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

```
- Symlink apache conf
```bash
ln -s /etc/apache2/sites-available/abimanyu.it22.com /etc/apache2/sites-enabled/abimanyu.it22.com
```
- Restart apache
```bash
service apache2 restart
```

## Nomer 12
> Setelah itu ubahlah agar url www.abimanyu.yyy.com/index.php/home menjadi www.abimanyu.yyy.com/home.

- Add config alias
```bash
# /etc/apache2/site-available/abaimanyu.it22.com
...
    Alias "index.php/home" "/var/www/abimanyu.it22/home.html"
...
```

## Nomer 13
> Selain itu, pada subdomain www.parikesit.abimanyu.yyy.com, DocumentRoot disimpan pada /var/www/parikesit.abimanyu.yyy
- Download file then unzip

```bash
wget -O /root/parikesit.zip "https://drive.usercontent.google.com/download?id=17tAM_XDKYWDvF-JJix1x7txvTBEax7vX&export=download&authuser=0&confirm=t&uuid=e1ee8117-918e-4a79-880c-7e7f9f14767a&at=APZUnTUybl6ig4kiWHRb7ghy3N0p:1697383050378"

uznip /root/parikesit.zip
```
- Copy file to /var/www
```bash
cp -r /root/parikesit.abimanyu.yyy.com /var/www/parikesit.abimanyu.it22
```
- Create apache config
```bash
# /etc/apache2/site-available/parikesit.abaimanyu.it22.com
<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/parikesit.abimanyu.it22
        ServerName parikesit.abimanyu.it22.com
        ServerAlias www.parikesit.abimanyu.it22.com

        <Directory /var/www/parikesit.abimanyu.it22/public>
            Options +Indexes
        </Directory>

        <Directory /var/www/parikesit.abimanyu.it22/secret>
            Options -Indexes
        </Directory>

        <LocationMatch "^/secret$">
            Order Deny,Allow
            Deny from all
        </LocationMatch>

        Alias "/js" "/var/www/parikesit.abimanyu.it22/public/js"

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        ErrorDocument 404 /error/404.html
        ErrorDocument 403 /error/403.html
</VirtualHost>

```
- Symlink apache conf
```bash
ln -s /etc/apache2/sites-available/parikesit.abimanyu.it22.com /etc/apache2/sites-enabled/parikesit.abimanyu.it22.com
```
- Restart apache
```bash
service apache2 restart
```

## Nomer 14
> Pada subdomain tersebut folder /public hanya dapat melakukan directory listing sedangkan pada folder /secret tidak dapat diakses (403 Forbidden).
-   Add rule for direcoty listing /public
```bash
# /etc/apache2/site-available/parikesit.abaimanyu.it22.com
...
    <Directory /var/www/parikesit.abimanyu.it22/public>
        Options +Indexes
    </Directory>
...
```
- Add rule to deny /secret
```bash
# /etc/apache2/site-available/parikesit.abaimanyu.it22.com
...
    <LocationMatch "^/secret$">
        Order Deny,Allow
        Deny from all
    </LocationMatch>
...
```

## Nomer 15
> Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.

- Add rule to map error template file
```bash
# /etc/apache2/site-available/parikesit.abaimanyu.it22.com
...
    ErrorDocument 404 /error/404.html
    ErrorDocument 403 /error/403.html
...
```

## Nomer 16
> Buatlah suatu konfigurasi virtual host agar file asset www.parikesit.abimanyu.yyy.com/public/js menjadi www.parikesit.abimanyu.yyy.com/js 
```bash
# /etc/apache2/site-available/parikesit.abaimanyu.it22.com
...
    Alias "/js" "/var/www/parikesit.abimanyu.it22/public/js"
...
```

## Nomer 17
> Agar aman, buatlah konfigurasi agar www.rjp.baratayuda.abimanyu.yyy.com hanya dapat diakses melalui port 14000 dan 14400.
- Download file then unzip

```bash
wget -O /root/rjp.baratayuda.abimanyu.zip "https://drive.usercontent.google.com/download?id=17tAM_XDKYWDvF-JJix1x7txvTBEax7vX&export=download&authuser=0&confirm=t&uuid=e1ee8117-918e-4a79-880c-7e7f9f14767a&at=APZUnTUybl6ig4kiWHRb7ghy3N0p:1697383050378"

uznip /root/rjp.zip
```
- Copy file to /var/www
```bash
cp -r /root/rjp.baratayuda.abimanyu.yyy.com /var/www/rjp.baratayuda.abimanyu.it22
```
- Create apache config
```bash
# /etc/apache2/site-available/rjp.baratayuda.abaimanyu.it22.com

<VirtualHost *:14000>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/rjp.baratayuda.abimanyu.it22
        ServerName rjp.baratayuda.abimanyu.it22.com
        ServerAlias www.rjp.baratayuda.abimanyu.it22.com

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        <Directory "/var/www/rjp.baratayuda.abimanyu.it22">
              AuthType Basic
              AuthName "Restricted Content"
              AuthUserFile /etc/apache2/.htpasswd
              Require valid-user
        </Directory>

</VirtualHost>

<VirtualHost *:14400>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/rjp.baratayuda.abimanyu.it22
        ServerName rjp.baratayuda.abimanyu.it22.com
        ServerAlias www.rjp.baratayuda.abimanyu.it22.com

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        <Directory "/var/www/rjp.baratayuda.abimanyu.it22">
              AuthType Basic
              AuthName "Restricted Content"
              AuthUserFile /etc/apache2/.htpasswd
              Require valid-user
        </Directory>

</VirtualHost>

<VirtualHost *:*>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/rjp.baratayuda.abimanyu.it22
        ServerName rjp.baratayuda.abimanyu.it22.com
        ServerAlias www.rjp.baratayuda.abimanyu.it22.com

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        <Location />
                Order deny,allow
                Deny from all
        </Location>

</VirtualHost>
```
- Symlink apache conf
```bash
ln -s /etc/apache2/sites-available/rjp.baratayuda.abimanyu.it22.com /etc/apache2/sites-enabled/rjp.baratayuda.abimanyu.it22.com
```
- Restart apache
```bash
service apache2 restart
```

## Nomer 18
> Untuk mengaksesnya buatlah autentikasi username berupa “Wayang” dan password “baratayudayyy” dengan yyy merupakan kode kelompok. Letakkan DocumentRoot pada /var/www/rjp.baratayuda.abimanyu.yyy.
- Install deps
```bash
sudo apt install apache2-utils
```
- Create credential
```bash
htpasswd /etc/apache2/.htpasswd Wayang baratayudait22
```
- Add rule to apache conf 
```bash
# /etc/apache2/site-available/rjp.baratayuda.abaimanyu.it22.com
...
        <Directory "/var/www/rjp.baratayuda.abimanyu.it22">
              AuthType Basic
              AuthName "Restricted Content"
              AuthUserFile /etc/apache2/.htpasswd
              Require valid-user
        </Directory>
...

```

- Restart apache2
```bash
service apache2 restart
```

## Nomer 19
> Buatlah agar setiap kali mengakses IP dari Abimanyu akan secara otomatis dialihkan ke www.abimanyu.yyy.com (alias)

- Add rule to apache conf

```apacheconf
# /etc/apache2/site-available/abaimanyu.it22.com
...
    ServerAlias 192.244.2.6
...
```

- Restart apache2
```bash
service apache2 restart
```

## Nomer 20
>

- Add rule `.htaccess`
```bash
# /var/www/parikesit.abimanyu.it22.com
RewriteEngine On
RewriteRule ^/public/image.*abimanyu.* /public/image/amibanyu.jpg [L,R=301]
```
- Enable mod rewrite
```bash
a2enmod rewrite
```
- Restart apache
```bash
service apache2 restart
```