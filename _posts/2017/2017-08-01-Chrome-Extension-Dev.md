---
layout: post
category : article
title : Chrome Extension Develop
tags : [Chrome]
---

## 簡述 
因工作Case關係接觸[Chrome Extension](https://developer.chrome.com/extensions)開發，如果有寫過[Tampermonkey](https://tampermonkey.net/)的Script，會感覺得有些概念及使用方式很相似，但多了更多**Browser**進階的操作及控制。

## Skill
- [JavaScript](https://developer.mozilla.org/zh-TW/docs/Learn/JavaScript)
- [Chrome DevTools](https://developer.chrome.com/devtools)

## 環境
- [Chrome Browser](https://www.google.com.tw/chrome/browser/desktop/index.html)

## 工具
- [VSCode](https://code.visualstudio.com/)

## 基本介紹

- ### [manifest.json](https://developer.chrome.com/extensions/manifest)
    - [manifest_version](https://developer.chrome.com/extensions/manifest/manifest_version)
        - 設定Chrome版本是否為**18**以上，是則配置 `2`
        - `"manifest_version": 2`
    - [name](https://developer.chrome.com/extensions/manifest/name#name)
        - 設定套件名稱，最多45個字元 
        - `"name": "Leo Extension"`
    - [version](https://developer.chrome.com/extensions/manifest/version)
        - 套件版號，可確保使用者版本最要設定啊! 
        - `"version": "0.1"`
    - [description](https://developer.chrome.com/extensions/manifest/description)
        - 套件描述，在[套件管理列表](chrome://extensions)可以看到描述內容
        - `"description": "Leo Tools"`
    - [icons](https://developer.chrome.com/extensions/manifest/icons)
        - 套件使用相關icon，主要三種格式 
            - 16*16 → 使用位置在套件頁面的 **favicon** 的圖示
            - 48*48 → 使用在[套件管理列表](chrome://extensions)的圖示
            - 128*128 → 使用在Store安裝時的圖示
        - ` "icons": {"16": "icon16.png","48":  "icon48.png","128": "icon128.png"} `
    - [background](https://developer.chrome.com/extensions/background_pages)
        - Html
        - Js
    - [permissions](https://developer.chrome.com/extensions/declare_permissions)
        - 套件授予權限，可操控通知訊息或是操作 **storage** 等。
        - `"permissions": ["storage","notifications"]`
    - [browser_action](https://developer.chrome.com/extensions/browserAction)
        - 套件工具列圖示及顯示頁面，可不設定此配置，但就不會顯示相關內容。
            - 
            ```
            "browser_action": {
                "default_title": "Leo Extension",
                "default_icon": "icon16.png",
                "default_popup": "popup.html"
            } 
            ```
            - <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170801/0001.png" alt="0001"/>
    - [content_scripts](https://developer.chrome.com/extensions/content_scripts)
       - 套件提供附加js、css至當前使用者瀏覽頁面，還可以指定特定網址(`matches`)戴入及時間(`run_at`)

       ```
       "content_scripts": [
        {
            "run_at": "document_end",
            "matches": [
                "http://www.google.com/*"
            ],
            "css": [
                "base.css"
            ],
            "js": [
                "jquery.js",
                "base.js"
            ]
        }]
        ```

    - [web_accessible_resources](https://developer.chrome.com/extensions/manifest/web_accessible_resources)
        - 供存取套件資源使用
        - ` "web_accessible_resources": ["base.css","base.js"] `

    - [content_security_policy](https://developer.chrome.com/extensions/contentSecurityPolicy)
        - 可設定白名單使用js等，例如可用cdn掛載的jquery更多例子可看(mozilla)[https://developer.mozilla.org/en-US/Add-ons/WebExtensions/manifest.json/content_security_policy]，或是看之後練習題目：`郵地區號五碼查詢`
        - 預設為 `"content_security_policy":"script-src 'self'; object-src 'self'"`

## 實作

- 練習題目 **郵地區號五碼查詢** (Quiz Taiwan zipcode)
    - 提供popup查詢功能 (popup query text)
    - 郵地區號API來源 [http://zip5.5432.tw/](http://zip5.5432.tw/) (Taiwan zipcode API Source)
    - 套件畫面 (View Chrome Extension)

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170801/0003.png" alt="0003"/>

    - 專案目錄檔案 (Project folder)

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170801/0004.png" alt="0004"/>

    - 專案程式碼 (Code files )

    <script src="https://gist.github.com/leejulee/43ecefbb11d1ba6b8b3726325c82e028.js"></script>
    
    OR 

    [GitHub Demo v1](https://github.com/leejulee/LeoChromeExtension/tree/5bc41fa129da4b063ed312678ec2ea66cb129912)

    - 我們因使用 [http://zip5.5432.tw/](http://zip5.5432.tw/) API加使用jsonp，所以需要在 **content_security_policy**設定白名單 

    ``` 
    "content_security_policy":"script-src 'self' https://zip5.5432.tw/; object-src 'self'" 
    ```

     否則就會爆下圖錯誤
     
     <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170801/0002.png" alt="0002"/>

    - 載入本機套件 (Load local folder)
        - 打開套件管理列表 (Open Extension Management) `chrome://extensions/`
        - 載入本機套件步驟 (Load local folder the steps)

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170801/0005.png" alt="0005"/>

    - 相關資訊 (reference & resource)
        - [開放資料 3+2碼郵遞區號](https://data.gov.tw/dataset/5948)
        - [台灣 3+2郵遞區號 查詢](http://zip5.5432.tw/)

- 練習題目 **郵地區號五碼查詢 V2** (Quiz Taiwan zipcode version 2)
    - 提供選取文字的右鍵查詢功能 (context menu query text)
    - 提供查詢記錄 (query zipcode history)
    - 套件畫面 (View Chrome Extension)
        
        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170801/0006.png" alt="0006"/>
        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170801/0007.png" alt="0007"/>
        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170801/0008.png" alt="0008"/>
        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170801/0009.png" alt="0009"/>

    - 專案程式碼 (Code files )

    <script src="https://gist.github.com/leejulee/9e461471e994899ac41cc377cbd01036.js"></script>

    OR 

    [GitHub Demo v2](https://github.com/leejulee/LeoChromeExtension)