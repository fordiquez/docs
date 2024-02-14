# MySQL

```shell
sudo apt update && sudo apt upgrade
```

```shell
sudo apt install mysql-server
```

```shell
sudo service mysql start
```

```shell
mysql
```

```mysql
CREATE USER 'username'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' WITH GRANT OPTION;
```

```mysql
FLUSH PRIVILEGES;
```

```shell
exit
```

```shell
mysql -u username -p
```

```shell
service mysql status
```
