# SSL

```shell
sudo snap install core
```

```shell
sudo snap refresh core
```

```shell
sudo apt remove certbot
```

```shell
sudo snap install --classic certbot
```

```shell
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

```shell
sudo nginx -t
```

```shell
sudo systemctl reload nginx
```

```shell
sudo ufw status
```

```shell
sudo ufw allow 80
```

```shell
sudo ufw allow 443
```

```shell
sudo ufw allow 22
```

```shell
sudo ufw enable
```

```shell
sudo ufw status
```

```shell
sudo certbot --nginx -d domain.com -d www.domain.com
```

```shell
sudo systemctl status snap.certbot.renew.service
```

```shell
sudo certbot renew --dry-run
```
