# Connect to EC2 Staging Server
```bash
sudo yum update -y
sudo yum install -y httpd24 php56 git unzip zip php56-curl postfix mailutils php56-json php56-mysqlnd php56-mbstring.x86_64 mod24_ssl php56-devel php56-gd php-pear ImageMagick ImageMagick-devel php56-pecl-imagick -y
sudo service httpd start
```
