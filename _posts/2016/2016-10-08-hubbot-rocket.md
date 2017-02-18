---
layout: post
category : article
title : hubot Rocket (記錄)
tags : [Javascript]
---

## 簡述
hubot是個開源的機器人框架，像是Salck、RocketChat這類的團隊溝通平台，就用來處理簡易查詢或教學使用，因本人目前使用rocket平台，就來寫個rocket hubot記錄吧！

## 環境準備
- install [node.js、npm](https://nodejs.org/en/)

## Skill
- [coffeejs](http://coffeescript.org/)
- [Regex](https://zh.wikipedia.org/wiki/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)

## hubot (RocketChat)
1. 安裝套件 `npm install -g yo generator-hubot`
2. 建立資料夾 ex : demohubot
3. 安裝腳本 `yo hubot --adapter="rocketchat@1"`

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161008/0001.png" alt="0001"/>
4. 設定hubot資訊(windows),打開 \bin\hubot.cmd，加上以下資訊

    ```
    set ROCKETCHAT_ROOM=general
    set LISTEN_ON_ALL_PUBLIC=true
    set ROCKETCHAT_USER=Rocket.bot
    set ROCKETCHAT_PASSWORD=xxxx
    set ROCKETCHAT_AUTH=password
    set ROCKETCHAT_URL=127.0.0.1:3010 
    ```
    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161008/0002.png" alt="0002"/>

    > RocketChat 需先建立 Rocket.bot 帳戶    
5. 腳本修改 `\scripts\example.coffee`

    ```
    robot.hear /hi/i, (res) ->
        res.send "hi"
    ```
    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161008/0004.png" alt="0004"/>
6. run `.\bin\hubot.cmd -a rocketchat`

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161008/0003.png" alt="0003"/>
7. 與bot聊天測試結果
 
    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20161008/0005.png" alt="0005"/>

## 參考資料
- [hubot](https://hubot.github.com/docs/)
- [hubot adapter](https://hubot.github.com/docs/adapters/)