# Key:
- wyomind
``` cmd
composer config repositories.wyomind composer https://support_sci_sport_co_uk:7db17e3cb0a1e5dbdb18e571@repo.wyomind.com
```
- amasty:
	- user 
	```
	d411240c7e5cd7f770aab5461a231358
	```
	- pass 
	```
	f91314643691771610d03edb97a3c1ca
	```
- plumrocket
	- user 
	```
	TNq06I9VNR2IyuRaLQd5VRUujKjKU20q
	```
	- pass 
	```
	J5BIXJg7sCJAiJIK5EwtxYyxrh8L8Ka4
	```

- magento:
	```
	composer global config http-basic.repo.magento.com 5153dc1fb153da4679ae7afe17714998 ce92519abfeeaf34fe5ad11c43d5b9bd
	```

- hockeyfactoryshop.co.uk:
```
ssh sg.hockeyfactoryshop.co.uk@80.66.202.202  -p2020

R7J3D9A3qKqY
```



# Cài đặt magento:
## Cách 1: Cài đặt bằng composer
### Step 1:
```
composer install
```
### Step 2:
```cmd
bin/magento setup:install \
--base-url=http://burning.loc/ \
--db-host=mysql \
--db-name=burningsite \
--db-user=root \
--db-password= \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@admin.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_US \
--currency=USD \
--timezone=America/Chicago \
--use-rewrites=1 \
--search-engine=elasticsearch7 \
--elasticsearch-host=172.16.238.240 \
--elasticsearch-port=9200 \
--elasticsearch-index-prefix=magento2 \
--elasticsearch-timeout=15 



```
**=> Hoàn tất**

## Cách 2: khi đã đầy đủ
### Step 1: 
```cmd
php bin/magento s:d:c
```

# Cài đặt database với dung lượng lớn:
```cmd
gunzip -c {url.sql.zip} | mysql -h localhost -P 3306 --protocol=tcp -u {user-name} -p {database-name}

mysql -h localhost -P 3306 --protocol=tcp -u root -p {dataname} < {url.sql}
```
------------------------------------------------------------------------------------------

# Cài đặt devilbox:
## Docker, docker composer

Mở terminal và run lần lượt các command line sau:
```cmd
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
=> Hoàn thành việc cài đặt docker và docker compose. Kiểm tra: `docker-compose --version`

## Devilbox
Dowload file và giải nén trong thư mục `var/www/`` (nếu chưa có thư mục thì tạo thư mục `www` - `sudo mkdir /var/www/``)

https://drive.google.com/file/d/1r3SzmKvK3KANlgOBvjb3T2OcN0eE6qLw/view?usp=share_link

Coppy file `docker-compose.override.yml` trong thư mục `compose` ra thư mục devilbox

run lệnh: `sudo chmod 777 -R devilbox/`

để cấp quyền cho thư mục. Sau đó truy cập thư mục devilbox: `cd devilbox/`

sửa file run.sh:
	*docker-compose up -d php httpd mysql elasticsearch;* --> *docker-compose up -d php httpd mysql elastic;*	

Run: `sudo sh run.sh`

=> Nếu thành công thì terminal sẽ như sau:
![img/img.png](img/img.png)

Lưu ý là các câu lệnh từ giờ sẽ chỉ được run trong phạm vi terminal này, `/shared/httpd` <=> `/var/www/devilbox/data/www/``

## Cách tạo một project mới

Tạo một thư mục mới trong `/var/www/devilbox/data/www/` (tên thư mục sẽ tương đương với tên miền của project)

Ví dụ: folder name là `test` => tên miền sẽ là:test.loc

##### Cấu trúc một thư mục project mới:
|—> tên project
|———> htdocs (tên mặc định)
|———> pub (tên mặc định) sẽ chứa các mã php, css, html ….

Sau bước này cần đăng ký tên miền trong file host ở commad line nhập như sau:
```cmd
sudo subl /etc/hosts
```

sau đó thêm dòng mới theo như sau:
```
127.0.0.1	<project-name>.loc
```
![img/img_1.png](img/img_1.png)
Sau đó có thể truy cập http://test.loc để kiểm tra

Một số tính năng cần chú ý trong devilbox:
- http://localhost/vhosts.php : vị trí danh sách các vitual host (project) đã được khởi tạo thành công
- http://localhost/index.php : thông tin chung của devilbox
- https://i.imgur.com/HnpkC1d.png : vị trí để truy cập phpmyadmin
Các hostname:
- Mysql: mysql
- Elasticsearch: elastic

## Cài đặt Magento 2
https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/overview.html

- B1, tạo new devilbox project (Ex: magento2), tạo database  (magento2)
- B2, Đăng ký tài khoản Adobe: https://marketplace.magento.com/
- B3, truy cập my Adobe account: https://marketplace.magento.com/customer/account/

để tạo các adobe key:
![img/img_2.png](img/img_2.png)

=> Create A New Access Key:
![img/img_3.png](img/img_3.png)

- B4: truy cập devilbox terminal ( https://i.imgur.com/yNIk1q0.png ) và truy cập đến project mới được tạo ( Ex: cd magento2/ )

run termial sau:
```cmd
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=<version> <install-directory-name>
```
Ex:
```cmd
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.4.6-p3 htdocs/
```

Lưu ý nếu gặp vân đề sau:
![img/img_4.png](img/img_4.png)

Thì cần thực hiện run thêm các command line sau:
```cmd
composer global config http-basic.repo.magento.com <public_key> <private_key>
```
My key:
- public_key: 5153dc1fb153da4679ae7afe17714998
- private_key: ce92519abfeeaf34fe5ad11c43d5b9bd

Sau đó tiếp tục run lại lệnh create ở trên

Sau khi thành công tải Magento => truy cập vào thư mục htdocs để tiếp tục các bước cài đặt site: `cd htdocs/``

Cấp quyền cho các thư mục cần thiết:
```cmd
sudo find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +
sudo find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +
sudo chown -R :www-data . 
sudo chmod u+x bin/magento

php bin/magento setup:install \
--base-url=http://web-name.loc \
--db-host=localhost \
--db-name=magento2 \
--db-user=root \
--db-password=admin \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@admin.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_US \
--currency=USD \
--timezone=America/Chicago \
--use-rewrites=1 \
--search-engine=elasticsearch7 \
--elasticsearch-host=localhost \
--elasticsearch-port=9200 \
--elasticsearch-index-prefix=magento2 \
--elasticsearch-timeout=15 
```

tham khảo về magento2 command line:
```link
https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/config-cli.html
```

Sau đó cần khai báo vitual host trong file hosts là có thể kiểm tra:
- frontend site: http://magento2.loc
- backend site: http://magento2.loc/admin <có thể tìm backend frontName ở file htdocs/app/etc/env.php - https://i.imgur.com/bKRB1uy.png  >

*Lưu ý:* để connect vào backend thì cần thiết lập hoặc tắt module `Magento_TwoFactorAuth` ( ở giai đoạn này thì nên tắt )

## Cách hiển thị lỗi trong Magento 2:

1. htdocs/app/bootstrap.php  - https://i.imgur.com/r9htTVD.png
![img/img_5.png](img/img_5.png)

2. Đổi tên trong thư mục htdocs/pub/errors:
`local.xml.sample ` -> `local.xml`
3. Đổi Magento mode sang developer (dev-mode)
```cmd
bin/magento deploy:mode:set developer
```

https://dev.southland.com.au/

### CLI Magento Basic:
```cmd
php -d memory_limit=-1 bin/magento {simple}:deploy
php bin/magento set:inst
php -d memory_limit=-1 bin/magento setup:upgrade

# Khởi tạo các static view file trong thư mục pub/:
sudo php -d memory_limit=-1 bin/magento setup:static-content:deploy -f

# Khởi tạo các file cần biên dịch:
sudo php -d memory_limit=-1 bin/magento setup:di:compile

# Flush Magento cache: 
php -d memory_limit=-1 bin/magento cache:flush

# Flush Cache Storage: 
php -d memory_limit=-1 bin/magento cache:clean

php -d memory_limit=-1 bin/magento index:reindex
```


---------------------------------------------------------------------------
## Upgrade module

```cmd
cp composer.json composer.json.bak
composer remove magento/product-community-edition --no-update
composer require magento/composer-root-update-plugin ~2.0 --no-update
composer require-commerce magento/product-community-edition 2.4.6-p3 --no-update
```

- In `composer.json`:

https://github.com/magento/magento2/blob/2.4.6-p1/composer.json

- Require:

https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html

```cmd
composer update 
```

- sau khi chạy xong xuất hiện như hình là bạn đã ok.
- Lưu ý phần upgrade chỉ cho source code magento không có cài extension bên thứ 3. Có thể thấy ở đây

![img.png](img.png)

- Sau khi upgrade xong cần đổi version trong file composer json

Tham khảo bài viết thêm ở đây:

https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/implementation/perform-upgrade.html

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Deploy:


- maria-db:
```cmd
sudo mysql -u root -p
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' IDENTIFIED BY 'admin' WITH GRANT OPTION;
FLUSH PRIVILEGES;
exit
mysql -u root -p
```

sudo apt-get install php8.2 libapache2-mod-php8.2 php8.2-bcmath php8.2-common php8.2-mbstring php8.2-xmlrpc php8.2-soap php8.2-gd php8.2-xml php8.2-intl php8.2-mysql php8.2-cli php8.2-ldap php8.2-zip php8.2-curl wget curl unzip -y


sudo find . -type f -exec chmod 644 {} \;            

sudo find . -type d -exec chmod 755 {} \;        

sudo chmod -Rf 777 var

sudo chmod -Rf 777 pub/static

sudo chmod -Rf 777 pub/media

sudo chmod 777 ./app/etc

sudo chmod 644 ./app/etc/*.xml
sudo chmod -Rf 775 bin


sudo chmod -Rf 777 ./*
sudo chown -Rf www-data:www-data ./*


### Config sshd:
```cmd
ssh-keygen -f "/home/buck/.ssh/known_hosts" -R "35.187.229.143"

sudo nano /etc/ssh/sshd_config
sudo usermod -aG sudo truongtbc
sudo passwd root
```

### Install php:
```cmd
sudo apt install ca-certificates apt-transport-https software-properties-common lsb-release -y
sudo add-apt-repository ppa:ondrej/php -y

sudo apt update
sudo apt install php8.2 libapache2-mod-php8.2 -y
sudo apt install php8.2-fpm libapache2-mod-fcgid

sudo apt-get install php8.2 libapache2-mod-php8.2 php8.2-bcmath php8.2-common php8.2-mbstring php8.2-xmlrpc php8.2-soap php8.2-gd php8.2-xml php8.2-intl php8.2-mysql php8.2-cli php8.2-ldap php8.2-zip php8.2-curl wget curl unzip -y

#apache
sudo a2enmod proxy_fcgi setenvif
sudo a2enconf php8.2-fpm
sudo systemctl restart apache2
```

### Mariadb
```cmd
sudo apt update && sudo apt upgrade -y
sudo apt install software-properties-common -y
wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2_amd64.deb
sudo dpkg -i libssl1.1_1.1.1f-1ubuntu2_amd64.deb
curl -LsS -O https://downloads.mariadb.com/MariaDB/mariadb_repo_setup
sudo bash mariadb_repo_setup --os-type=ubuntu  --os-version=focal --mariadb-server-version=10.6
wget http://ftp.us.debian.org/debian/pool/main/r/readline5/libreadline5_5.2+dfsg-3+b13_amd64.deb
sudo dpkg -i libreadline5_5.2+dfsg-3+b13_amd64.deb
sudo apt update
sudo apt install mariadb-server mariadb-client -y
sudo systemctl start mariadb
sudo systemctl enable mariadb

sudo mysql -u root -p
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' IDENTIFIED BY 'admin' WITH GRANT OPTION;
FLUSH PRIVILEGES;
exit
mysql -u root -p
```

### Conf elastic search:
```cmd
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
sudo apt update
sudo apt install elasticsearch
sudo systemctl start elasticsearch
sudo systemctl enable elasticsearch
```

### Conf Composer
```cmd
sudo apt update
sudo apt install php-cli unzip

curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
HASH=`curl -sS https://composer.github.io/installer.sig`
php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer
composer -V

```


### Conf Apache:
```cmd
sudo nano /etc/apache2/sites-available/burning.conf
<VirtualHost *:80>
    ServerAdmin batruong1704@gmail.com
    DocumentRoot /var/www/html/htdocs/pub/
    ServerName burninghotel.click

    <Directory /var/www/html/pub>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
sudo a2ensite burning.conf
sudo a2enmod rewrite
sudo systemctl restart apache2
sudo systemctl reload apache2

sudo tail /var/log/apache2/

```

### Conf Magento
```cmd
sudo a2ensite magento.conf
sudo php -d memory_limit=-1 bin/magento setup:upgrade
# Khởi tạo các static view file trong thư mục pub/:
sudo php -d memory_limit=-1 bin/magento setup:static-content:deploy -f
# Khởi tạo các file cần biên dịch:
sudo php -d memory_limit=-1 bin/magento setup:di:compile
# Flush Magento cache:
sudo php -d memory_limit=-1 bin/magento cache:flush
# Flush Cache Storage:
sudo php -d memory_limit=-1 bin/magento cache:clean
sudo php -d memory_limit=-1 bin/magento index:reindex

sudo bin/magento deploy:mode:set developer
```

<VirtualHost *:80>
   ServerName          mysite.mg
   DocumentRoot        /var/www/html/magento2/pub/
</VirtualHost>

<VirtualHost *:443>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html/pub
        ServerName dn.burninghotel.click

        SetEnv MAGE_RUN_CODE "HN"
        SetEnv MAGE_RUN_TYPE "Store"

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access_staging.log combined

        SSLEngine on
        SSLCertificateFile /etc/apache2/ssl/burninghotel.click.pem
        SSLCertificateKeyFile /etc/apache2/ssl/burninghotel.click.key
        <Directory /var/www/html/pub>
                Options Indexes FollowSymLinks
                AllowOverride All
                Require all granted
        </Directory>

</VirtualHost>



<VirtualHost *:80>
        ServerName hn.burninghotel.click
        DocumentRoot /var/www/html/pub
        SetEnv MAGE_RUN_CODE "HN"
        SetEnv MAGE_RUN_TYPE "HN"
         <Directory /var/www/html/pub>
                Options Indexes FollowSymLinks
                AllowOverride All
                Require all granted
        </Directory>
</VirtualHost>

tạo 1 branch mới (uk-newbranch) -> request -> báo anh review