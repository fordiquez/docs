# Nginx

## 1. Install & config nginx

```shell
sudo apt-get update && apt-get upgrade
```

```shell
sudo apt install nginx
```

```shell
sudo nano /etc/nginx/sites-available/domain.com
```

### 1.1 Back-end config
```nginx configuration
server {
    server_name domain.com;
    root /var/www/elephant/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php index.html;

    charset utf-8;

    client_max_body_size 50M;

    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
    
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    # Fixing livewire not found error
    location = /livewire/livewire.js {
        expires off;
        try_files $uri $uri/ /index.php?$query_string;
    }

    # Block access to build scripts.
    location ~* /(Gruntfile\.js|package\.json|node_modules) {
        deny all;
        return 404;
    }

    # Add cache headers for site assets.
    location ~* \.(?:ico|css|js|gif|jpe?g|png|eot|woff|ttf)$ {
        expires 30d;
        add_header Pragma public;
        add_header Cache-Control "public";
    }

    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/run/php/php8.3-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $request_filename;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

### 1.2 Front-end config

```nginx configuration
server {
    listen 80;
    server_name domain.com;
    root /var/www/app/dist;
    index index.html;
    
    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
    include mime.types;

    location / {
        root /var/www/myapp/dist;
        try_files $uri  /index.html;
    }
}
```

```shell
sudo mkdir /var/www/domain.com
```

```shell
sudo chown -R www-data:www-data /var/www/domain.com
```

```shell
sudo ln -s /etc/nginx/sites-available/yourdomain.com /etc/nginx/sites-enabled/
```

```shell
sudo service nginx restart
```

## 2. Redirect from www to non-www

### 2.1 First way

```shell
sudo nano /etc/nginx/sites-available/my-website.com.conf
```

```nginx configuration
server {
    server_name my-website.com;
}
```

```shell
sudo nano /etc/nginx/sites-available/www.my-website.com.conf
```

```nginx configuration
server {
    server_name www.my-website.com;
    return 301 $scheme://my-website.com$request_uri;
}
```

```shell
sudo ln -s /etc/nginx/sites-available/www.my-website.com.conf /etc/nginx/sites-enabled/
```

```shell
sudo nginx -t
```

```shell
sudo service nginx restart
```

```shell
curl -IL https://www.my-website.com
```

### 2.2 Second way

```shell
sudo nano /etc/nginx/conf.d/www.domain.conf
```

```nginx configuration
server {
    server_name www.domain.com;
    return 301 $scheme://domain.com$request_uri;
}

server {
    if ($host = www.domain.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    server_name www.domain.com;
    listen 80;
    return 404; # managed by Certbot
}
```

```shell
sudo nano /etc/nginx/sites-available/domain
```

```nginx configuration
server {
    if ($host = domain) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    listen 80;
    server_name domain.com;
    return 404; # managed by Certbot
}
```
