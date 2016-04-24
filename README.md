# Docker PHP5 + MYSQL

![Docker PHP5 + MYSQL](https://raw.githubusercontent.com/fuyuanli/Docker-PHP5-MySQL/master/web.png)

## 簡介

使用官方教學 [Docker Compose][1]  所建立的 PHP5 + MySQL 環境，使用之前請 **自行安裝 Docker Compose** ，基於以下兩個 image 建立:
   - [orchardup/php5][2]  
   - [orchardup/mysql][3]

網頁根目錄位於 `./html` 內，目前有放置一個 `index.php` 作為 Demo。  
資料庫的話預設帳號為 `root`，密碼為空(只有該容器可以讀取，沒有對外)，PHP 程式要連線 host 請使用 `db:3306` 進行連線。

## 使用方法

一開始請先下載此程式碼，並進入資料夾：

    $ git clobe https://github.com/fuyuanli/Docker-PHP5-MySQL.git
    $ cd Docker-PHP5-MySQL
    
#### build
依據腳本建立 Container：

    $ docker-compose build

    
看到類似以下的樣子就是完成了：

    db uses an image, skipping
    Building web
    Step 1 : FROM orchardup/php5
    ---> d8e.....8720
    Step 2 : ADD . /code
    ---> 179.....d553
    Removing intermediate container 1ec751450c87
    Successfully built 179ce51ed553

build 的 Container 加上 pull 下來的共會產生 6 個 image：

    orchardup/mysql         orchardup/mysql:latest  orchardup/php5          orchardup/php5:latest   web_web                 web_web:latest
 
#### 啟動容器

    $ docker-compose up

之後會直接執行

    Starting web_db_1
    Recreating web_web_1
    Attaching to web_db_1, web_web_1
    db_1   | 160424 13:36:41 [Warning] Using unique option prefix key_buffer ....
    .
    .
    db_1   | 160424 13:36:45 [Note]   - '0.0.0.0' resolves to '0.0.0.0';
    db_1   | 160424 13:36:45 [Note] Server socket created on IP: '0.0.0.0'.
    db_1   | 160424 13:36:45 [Note] Event Scheduler: Loaded 0 events
    db_1   | 160424 13:36:45 [Note] /usr/sbin/mysqld: ready for connections.
    db_1   | Version: '5.5.38-0ubuntu0.12.04.1-log'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  (Ubuntu)

#### 關閉容器
關閉的方法直接 Ctrl + C 就可以了：

    ^CGracefully stopping... (press Ctrl+C again to force)
    Stopping web_web_1 ... done
    Stopping web_db_1 ... done

#### 刪除容器
使用`docker rm` 、`docker rmi`即可刪除。

[1]:https://docs.docker.com/compose/
[2]:https://hub.docker.com/r/orchardup/php5/
[3]:https://hub.docker.com/r/orchardup/mysql/
