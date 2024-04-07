# docker-pgadmin4-tutorial

利用 docker 快速建立 pgadmin4 以及 Ubuntu 本機如何安裝 pgadmin4

* [Youtube Tutorial - 利用 docker 快速建立 pgadmin4](https://youtu.be/uewKHemeipE)

## 本機安裝 pgadmin4

pgadmin4 是連接 PostgreSQL 的 GUI 工具，

Linux 安裝 pgadmin4 在本機的方法可參考 [pgAdmin 4 (APT)](https://www.pgadmin.org/download/pgadmin-4-apt/)

```txt
#
# Setup the repository
#

# Install the public key for the repository (if not done previously):
sudo curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add

# Create the repository configuration file:
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'

#
# Install pgAdmin
#

# Install for both desktop and web modes:
sudo apt install pgadmin4

# Install for desktop mode only:
sudo apt install pgadmin4-desktop

# Install for web mode only:
sudo apt install pgadmin4-web

# Configure the webserver, if you installed pgadmin4-web:
sudo /usr/pgadmin4/bin/setup-web.sh
```

在 App 中可以看到 pgadmin4 的圖示

![alt tag](https://i.imgur.com/aPFxORg.png)

點他就會自動開啟了

![alt tag](https://i.imgur.com/y9KAk7R.png)

## docker 安裝 pgadmin4

使用 [dpage/pgadmin4](https://hub.docker.com/r/dpage/pgadmin4/) 這個 images，

```cmd
docker pull dpage/pgadmin4
```
使用已下指令建立

```cmd
docker run -p 5050:80 \
    -e "PGADMIN_DEFAULT_EMAIL=xxxrubiks@gmail.com" \
    -e "PGADMIN_DEFAULT_PASSWORD=SuperSecret" \
    -d dpage/pgadmin4
```

![alt tag](https://i.imgur.com/gEmZWsw.png)

輸入你設定的 email 和 password 登入

![alt tag](https://i.imgur.com/YLzy9QP.png)

![alt tag](https://i.imgur.com/nylk0Em.png)

## docker compose 安裝 pgadmin4

[docker-compose.yml](https://github.com/twtrubiks/docker-pgadmin4-tutorial/blob/master/docker-compose.yml) 版本,

如果你是使用 docker 內的 pgadmin4, 然後你想要連線到容器內的 db,

pgadmin4 的連線 host 要填 docker 的 service name,

以這個例子, host name 就是要填 `db`.

```yml
version: '3.5'

services:

  db:
      image: postgres:16.2
      # ports:
      #   - "5432:5432"
      environment:
        - POSTGRES_DB=postgres
        - POSTGRES_USER=postgres
        - POSTGRES_PASSWORD=postgres
        - PGDATA=/var/lib/postgresql/data/pgdata
      volumes:
        - db-data:/var/lib/postgresql/data/pgdata

  pgadmin4:
      container_name: my_pgadmin4
      image: dpage/pgadmin4
      restart: "always"
      environment:
        PGADMIN_DEFAULT_EMAIL: "YOUR@gmail.com"
        PGADMIN_DEFAULT_PASSWORD: "PASSWORD"
        PGADMIN_CONFIG_SESSION_EXPIRATION_TIME: 365
        PGADMIN_CONFIG_MAX_SESSION_IDLE_TIME: 60
      volumes:
        - pgadmin4-data:/var/lib/pgadmin
      ports:
        - "5050:80"
      extra_hosts:
        - "host.docker.internal:host-gateway"

volumes:
    db-data:
    pgadmin4-data:

```

更多的參數設定，文件可參考 [container_deployment](https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html)

## Reference

* [dpage/pgadmin4](https://hub.docker.com/r/dpage/pgadmin4/)

## Donation

文章都是我自己研究內化後原創，如果有幫助到您，也想鼓勵我的話，歡迎請我喝一杯咖啡:laughing:

綠界科技ECPAY ( 不需註冊會員 )

![alt tag](https://payment.ecpay.com.tw/Upload/QRCode/201906/QRCode_672351b8-5ab3-42dd-9c7c-c24c3e6a10a0.png)

[贊助者付款](http://bit.ly/2F7Jrha)

歐付寶 ( 需註冊會員 )

![alt tag](https://i.imgur.com/LRct9xa.png)

[贊助者付款](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## 贊助名單

[贊助名單](https://github.com/twtrubiks/Thank-you-for-donate)

## License

MIT license

