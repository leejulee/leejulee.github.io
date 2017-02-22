---
layout: post
category : article
title : Linux crontab 、vi 、python (記錄)
tags : [Linux,Python]
---

## 簡述
最近想試一下Linux的[crontab](https://zh.wikipedia.org/wiki/Cron)排程來定時發送訊息至[RocketChat](https://rocket.chat/)，順便學學Python及熟悉linux。

> DEMO環境：Linux os centos6 、 Python 2.6.6

## Skill
- Linux 
    - [vi](https://zh.wikipedia.org/wiki/Vi)
    - [crontab](https://zh.wikipedia.org/wiki/Cron)
- Python

## vi Command Line
- 不存檔離開(沒編輯可用)

    ```
    :q
    ```

- 強制不存檔離開(已編輯可用)

    ```
    :q!
    ```

- 存檔加離開

    ```
    :wq
    ```

- 開始編輯

    ```
    i
    ```

- 結束編輯

    ```
    esc
    ```

## crontab Command Line & example
- 查看排程列表

    ```
    crontab -l
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20160626/0001.png" alt="0001"/>

- 新增排程

    ```
    crontab -e
    ``` 

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20160626/0002.png" alt="0002"/>

- 固定排程案例說明
    - 格式說明： `分 時 日 月 星期 Command`
    - 格式可設定值區間：
        - 分：0-59
        - 時：0-23
        - 日：1-31
        - 月：1-12
        - 星期：0-6
        - Command：執行的command，這裡用執行python檔為例
    - 格式通用可設定值：
        - \* ：表示該欄位所有時間都可以
        - , ：表示該欄位多選項目時間都可以
    - 情境：星期一至五固定九點提醒訂便當
        - 設定值： `0 9 * * 1,2,3,4,5 /opt/orderlunch.py`

## Python Command Line & example
- 打開 python 程式語法

    ```
    python
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20160626/0005.png" alt="0005"/>

- 離開 python 程式語法

    ```
    exit()
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20160626/0006.png" alt="0006"/>

- 腳本指定環境執行python語法 ([Shebang (Unix)](https://en.wikipedia.org/wiki/Shebang_(Unix)))

    ```
    #!/usr/bin/env python
    ```

- 引用檔案語法

    ```
    import urllib
    import urllib2
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20160626/0004.png" alt="0004"/>

- 定義function語法

    ```
    def functionName(parameter):
        data=parameter
        return data
    ```

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20160626/0003.png" alt="0003"/>

- 腳本 orderlunch.py
    ```
    #!/usr/bin/env python

    import urllib
    import urllib2

    hookurl = 'http://RocketChat:3000/hooks';
    token = '/abcdefg/12345qazwsx';
    posturl = hookurl+token;

    def send_msg(msg):
        data = [('text',msg)]
        data = urllib.urlencode(data)
        req = urllib2.Request(posturl,data)
        req.add_header('Content-Type',application/x-www-form-urlencoded')
        response = urllib2.urlopen(req).red()
        return response;
    
    send_msg('remember order lunch!')
    ```

## 參考資料
- [鳥哥的 Linux 私房菜 - vi](http://linux.vbird.org/linux_basic/redhat6.1/linux_07vi.php)
- [Cron](https://zh.wikipedia.org/wiki/Cron)
- [鳥哥的 Linux 私房菜 - crontab](http://linux.vbird.org/linux_basic/0430cron.php)
- [Shebang (Unix)](https://en.wikipedia.org/wiki/Shebang_(Unix))
- [Python Basic Syntax](https://www.tutorialspoint.com/python/python_basic_syntax.htm)
- [Python Functions](https://www.tutorialspoint.com/python/python_functions.htm)