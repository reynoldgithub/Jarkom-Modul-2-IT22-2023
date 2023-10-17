# LAPORAN RESMI MODUL 3 JARKOM

-   Reynold Putra Merdeka | 5027211034






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

```bash
# /etc/apache2/site-available/abaimanyu.it22.com
...
    ServerAlias 192.244.2.6
...
```

- Restart apache2
```bash
service apache2 restart
```