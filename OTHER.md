# Redis, Supervisor, Task Scheduling, Chromium browser

### 1.1 Installing and Configuring Redis

```shell
sudo apt update && sudo apt upgrade
```

```shell
sudo apt install redis-server
```

```shell
sudo nano /etc/redis/redis.conf
```

```
# If you run Redis from upstart or systemd, Redis can interact with your
# supervision tree. Options:
#   supervised no      - no supervision interaction
#   supervised upstart - signal upstart by putting Redis into SIGSTOP mode
#   supervised systemd - signal systemd by writing READY=1 to $NOTIFY_SOCKET
#   supervised auto    - detect upstart or systemd method based on
#                        UPSTART_JOB or NOTIFY_SOCKET environment variables
# Note: these supervision methods only signal "process is ready."
#       They do not enable continuous liveness pings back to your supervisor.
supervised systemd
```

```shell
sudo systemctl restart redis.service
```

### 1.2 Testing Redis

```shell
sudo systemctl status redis
```

```shell
redis-cli
```

```redis
ping
```

### 1.3 Configuring a Redis Password

```shell
sudo nano /etc/redis/redis.conf
```

```shell
openssl rand 60 | openssl base64 -A
```

```
# requirepass foobared
```

```shell
sudo systemctl restart redis.service
```

```shell
redis-cli
```

```redis
auth your_redis_password
```

```redis
quit
```

## 2. Installing and Configuring Supervisor

```shell
sudo apt update && sudo apt upgrade
```

```shell
sudo apt install supervisor
```

```shell
sudo service supervisor restart
```

```shell
sudo systemctl enable supervisor
```

```shell
sudo nano /etc/supervisor/conf.d/horizon.conf
```

```
[program:horizon]
process_name=%(program_name)s
command=php /home/forge/example.com/artisan horizon
autostart=true
autorestart=true
user=forge
redirect_stderr=true
stdout_logfile=/home/forge/example.com/horizon.log
stopwaitsecs=3600
```

```shell
supervisorctl reread
```

```shell
supervisorctl update
```

```shell
supervisorctl restart all
```

```shell
supervisorctl start horizon
```

```shell
service supervisor restart
```

## 3. Set up schedule

```shell
crontab -e
```

```cronexp
* * * * * php /path/to/artisan schedule:run >> /dev/null 2>&1
```

```shell
sudo service cron restart
```

### 4. Installing Chromium browser

```shell
sudo apt install libxkbcommon0 libxshmfence1 ca-certificates fonts-liberation libasound2 libatk-bridge2.0-0 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgbm1 libgcc1 libglib2.0-0 libgtk-3-0 libnspr4 libnss3 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 lsb-release wget xdg-utils
```

```shell
sudo apt-get install chromium-browser
```
