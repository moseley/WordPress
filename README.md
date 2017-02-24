# Connect to EC2 Staging Server

## Basic setup with YUM
```bash
sudo yum update -y
sudo yum install httpd24 php56 git unzip zip php56-curl postfix mailutils php56-json php56-mysqlnd php56-mbstring.x86_64 mod24_ssl php56-devel php56-gd php-pear ImageMagick ImageMagick-devel php56-pecl-imagick -y
vim /etc/httpd/
sudo service httpd start
```

## Setup staging apache headers
```bash
sudo vim /etc/httpd/conf.d/000-default.conf
```

Paste the following:
```bash
<VirtualHost *:80>
        #ServerName example.com
        #ServerAlias www.example.com
        DocumentRoot /var/www/staging

        <Directory /var/www/staging>
                Options -Indexes
                AllowOverride All
                Order allow,deny
                Allow from all
        </Directory>
</VirtualHost>
```

Save:
```bash
ZZ
```

## Cleanup and prepare
```bash
cd /var/www/html
rm -rf *
cd ../
sudo mkdir staging
cd staging
sudo git clone https://github.com/moseley/wpelac.git .
sudo groupadd www
sudo usermod -a -G www ec2-user
exit
sudo usermod -a -G www apache
sudo chown -R apache /var/www
sudo chgrp -R www /var/www
sudo chmod 2775 /var/www
find /var/www -type d -exec sudo chmod 2775 {} \;
find /var/www -type f -exec sudo chmod 0664 {} \;
sudo service httpd restart
sudo chkconfig httpd on
```
