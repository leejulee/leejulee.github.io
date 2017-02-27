---
layout: post
category : article
title : Together Booard by docker & couchdb(記錄)
tags : [Docker,Couchdb]
---

## 簡述
因同事們已經習慣用 [微軟Lync](https://zh.wikipedia.org/wiki/Skype_for_Business) 通訊軟體上的共用白板，於是跟同事兩個一起做了陽春版的共用白版 (取名 [TogetherBoard](https://github.com/leejulee/TogetherBoard) ) 擴充至 [RocketChat](https://rocket.chat/) 來每個Channel使用，最近也已經包裝至 dockerhub ([docker-togetherboard](https://hub.docker.com/r/leejulee/docker-togetherboard/))，再安裝 dockerhub 的 [couchdb](https://hub.docker.com/r/klaemo/couchdb/)，就可以快速安裝使用囉！

> DEMO環境及系統：Linux os mint mate 18 、 docker 1.13.1 、 Couchdb 1.6.1 、 TogetherBoard

> linux 都用採 sudo -i 模式登入操作

## Skill

- [docker](https://www.docker.com/)
- couchdb
    - [couchdb](http://couchdb.apache.org/)
    - [couchdb dockerhub](https://hub.docker.com/r/klaemo/couchdb/)

## docker 
- 簡易說明此篇用到的 command line
    - [pull](https://docs.docker.com/engine/getstarted/step_six/#/step-2-pull-your-new-image) 取一個image檔案至本機
        -
    - [run](https://docs.docker.com/engine/reference/commandline/run/) 啟動一個image至container
        - [-p](https://docs.docker.com/engine/reference/commandline/run/#/publish-or-expose-port--p---expose) 設定 container port對應本機port的參數
        - [-d](https://docs.docker.com/engine/reference/commandline/run/#/options) container 執行在背景程式的參數
        - [-v](https://docs.docker.com/engine/reference/commandline/run/#/options) 梆定本機資料卷(原文：Bind mount a volume)與container的對應

## Couchdb

- 安裝 docker 位置：[couchdb (dockerhub)](https://hub.docker.com/r/klaemo/couchdb/)
- 安裝及設定：

    ```
    docker pull couchdb:latest
    docker run -d -p 5984:5984
    ```

- 打開配置修改設定
    - 配置頁面：
        
        `/_utils/config.html`

    - 修改 [enabling-cors](http://docs.couchdb.org/en/1.3.0/cors.html#enabling-cors) 
        
        ```
        httpd enable_cors true
        ```

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170225/0001.png" alt="0001"/>

    - 修改及新增參數 [passing-credentials](http://docs.couchdb.org/en/1.3.0/cors.html#passing-credentials)
        
        ```
        cors credentials true
        cors origins     *
        ```

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170225/0003.png" alt="0003"/>

        > origins 預設沒有這個欄位，需要另外新增，參考下圖新增方式

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170225/0002.png" alt="0002"/>

## Together Board

- 安裝 docker 位置： [docker-togetherboard (dockerhub)](https://hub.docker.com/r/leejulee/docker-togetherboard/)
    
    ```
    docker pull leejulee/docker-togetherboard
    docker run -d -p 3010:3010 leejulee/docker-togetherboard
    ```
- 共用白版畫面及分享說明
    - 啟動畫面

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170225/0006.png" alt="0006"/>

    - 共用說明
        - 如果在URL沒有代ID參數，預設會自動產生一組ID，可用Console查詢 `infoLocal._id`，如下圖

            <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170225/0005.png" alt="0005"/>

        - 如果要白板共用分享則需在url加上id，例如 `http://127.0.0.1:3010/?test-001`，再用不同browser或tab頁打開就會看到同一個內容囉！

            <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170225/0004.png" alt="0004"/>

## 原始碼
- [TogetherBoard](https://github.com/leejulee/TogetherBoard)
- [docker-togetherboard](https://github.com/leejulee/docker-togetherboard/)