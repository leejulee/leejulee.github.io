---
layout: post
category : article
title : dotnetcore deploy to ubuntu 14.04
tags : [.NET Core , ubuntu]
---

## 簡述 
練習.Net Core 佈署(採Framework-dependent deployments)至Ubuntu 14.04環境。

## Skill
- [Ubuntu](http://wiki.ubuntu-tw.org/index.php?title=%E9%A6%96%E9%A0%81)
- [Ubuntu 14.04 supervisord](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md#installing-supervisor)
- [.Net Core](https://docs.microsoft.com/zh-tw/dotnet/core/index)
- [.Net Core CLI](https://docs.microsoft.com/zh-tw/dotnet/core/tools/index?tabs=netcore2x)

## 環境
- Mac
- .Net Core 2.1
- Ubuntu 14.04

## Ubuntu 實作
- 首先安裝 .Net Core SDK [install .net core sdk to ubuntu 14.04](https://www.microsoft.com/net/download/linux-package-manager/ubuntu14-04/sdk-current)

    ```
    wget -q https://packages.microsoft.com/config/ubuntu/14.04/packages-microsoft-prod.deb
    sudo dpkg -i packages-microsoft-prod.deb
    ```

    ```
    sudo apt-get install apt-transport-https
    sudo apt-get update
    sudo apt-get install dotnet-sdk-2.1
    ```
    
- 確認安裝是否成功 (check dotnet) `dotnet --version` 
- 建立webapi專案 (create dotnet webapi project) `dotnet new webapi -o LeoAPI`
- 切換至專案資料夾 (switch folder) `cd LeoAPI/`
- 修改檔案 (modify file) **Startup.cs** 
    - 編輯檔案指令 (edit cmd) `nano Startup.cs`
    - 註解自動轉導https的設定 (mark https code) `// app.UseHttpsRedirection();`

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20180901/dotnetcore_0002.jpg" alt="dotnetcore_0002"/>

- 修改專案的配置 (modify file) **Properties/launchSettings.json**
    - 編輯檔案指令 (edit cmd) `nano Properties/launchSettings.json `

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20180901/dotnetcore_0003.jpg" alt="dotnetcore_0003"/>

    - 將檔案裡的 **localhost** 改為 **127.0.0.1** `"applicationUrl": "https://127.0.0.1:5001;http://127.0.0.1:5000"`

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20180901/dotnetcore_0004.jpg" alt="dotnetcore_0004"/>
    
- 建置專案 (build project)  `dotnet build`
- 執行專案 (run project) `dotnet run`

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20180901/dotnetcore_0007.jpg" alt="dotnetcore_0007"/>

- 建立發佈資料夾 (create publish folder) `mkdir /var/dotnetcore`
- 執行發佈指令至指定資料夾 (dotnet publish to publish folder) `dotnet publish /LeoAPI/LeoAPI.csproj -c Release -o /var/dotnetcore/`

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20180901/dotnetcore_0005.jpg" alt="dotnetcore_0005"/>

- 瀏覽發佈資料夾 (view publish folder) `ls /var/dotnetcore/`

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20180901/dotnetcore_0006.jpg" alt="dotnetcore_0006"/>

- 安裝 (install) supervisor `sudo apt-get install supervisor`
- 建立 (create) leoapi.conf `nano /etc/supervisor/conf.d/leoapi.conf`

    ```
    [program:leoapi]
    command=/usr/bin/dotnet /var/dotnetcore/LeoAPI.dll
    directory=/var/dotnetcore/
    autostart=true
    autorestart=true
    stderr_logfile=/var/log/leoapi.err.log
    stdout_logfile=/var/log/leoapiout.log
    environment=HOME=/var/www/,ASPNETCORE_ENVIRONMENT=Production
    user=www-data
    stopsignal=INT
    stopasgroup=true
    killasgroup=true
    ```
- 啟動服務 (start service) `sudo service supervisor start`
- 測試 (test) API `curl http://127.0.0.1:5000/api/values`

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20180901/ubuntu_0002.jpg" alt="0001"/>
- 停止服務 (stop service) `sudo service supervisor stop`