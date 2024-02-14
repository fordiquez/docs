# PHP 8.3 & Composer

## 1. PHP 8.3 installation
```shell
sudo apt install -y lsb-release ca-certificates apt-transport-https software-properties-common
```

```shell
sudo add-apt-repository ppa:ondrej/php
```

```shell
sudo apt-get update && apt-get upgrade
```

```shell
sudo apt install php8.3-fpm
```

```shell
sudo apt install -y php8.3-common php8.3-mysql php8.3-xml php8.3-xmlrpc php8.3-curl php8.3-gd php8.3-imagick php8.3-cli php8.3-dev php8.3-imap php8.3-mbstring php8.3-opcache php8.3-soap php8.3-zip php8.3-redis php8.3-intl php8.3-bcmath
```

```shell
sudo nano /etc/php/8.3/fpm/php.ini
```

```ini
max_execution_time = 600
max_input_time = 600
max_input_vars = 3000
memory_limit = 256M
post_max_size = 48M
upload_max_filesize = 48M
```

```shell
sudo service php8.3-fpm restart
```

## 2. Composer installation

```shell
curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
```

```shell
sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer
```
