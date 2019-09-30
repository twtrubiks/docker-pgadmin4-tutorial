# docker-pgadmin4-tutorial

利用 docker 快速建立 pgadmin4 以及 Ubuntu 本機如何安裝 pgadmin4

* [Youtube Tutorial - 利用 docker 快速建立 pgadmin4](https://youtu.be/uewKHemeipE)

## 本機安裝 pgadmin4

pgadmin4 是連接 PostgreSQL 的 GUI 工具，

Windows 安裝 pgadmin4 在本機的方法很簡單，可參考 [pgadmin-4-windows](https://www.pgadmin.org/download/pgadmin-4-windows/)。

Linux 安裝 pgadmin4 在本機的方法可參考 [PostgreSQL - Linux downloads (Ubuntu)](https://www.postgresql.org/download/linux/ubuntu/)

因為 pgadmin4 算是這個 repository 包含的第三方 addons，

安裝方法在這邊稍微說明一下，

先建立 `/etc/apt/sources.list.d/pgdg.list` 檔案並加入 repository

```cmd
sudo vim /etc/apt/sources.list.d/pgdg.list
deb http://apt.postgresql.org/pub/repos/apt/ YOUR_UBUNTU_VERSION_HERE-pgdg main
```

注意到這邊的 `YOUR_UBUNTU_VERSION_HERE`，要如何查看自己的版本，

執行已下指令

```cmd
lsb_release -a
```
![alt tag](https://i.imgur.com/Ps8bYwd.png)

這邊可以看到我的版本是 bionic，

所以就填入，

```cmd
deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main
```

再來是加入 repository signing key，然後更新 package lists

```cmd
sudo wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt update
```

最後就是安裝 pgadmin4

```cmd
sudo apt install pgadmin4
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

還有更多的參數可以設定，文件可參考 [container_deployment](https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html)。

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

