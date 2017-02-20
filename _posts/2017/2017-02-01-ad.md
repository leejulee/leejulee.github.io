---
layout: post
category : article
title : Active Directory Explorer & RocketChat LDAP (記錄)
tags : [Windows,Tools]
---

## 簡述
最近想試RocketChat的LDAP設定，但對於ad相關資訊又不是很了解，後來上網找到了一個工具：[AdExplorer](https://technet.microsoft.com/en-us/sysinternals/adexplorer.aspx)，它是個簡易查詢個人ad資訊的工具，大大減少撞牆及申請手續麻煩。

## Skill
- [Active Directory](https://zh.wikipedia.org/wiki/Active_Directory)

## AdExplorer
1. 打開 ADExplorer.exe 後，會需要連結到ADServer、個人帳密

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170201/0001.png" alt="0001"/>

2. 登入後資訊列表

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170201/0002.png" alt="0002"/>
3. Search 功能，以查詢使用者為例
    1. class 為 user
    2. attribute 為 [sAMAccountName](https://msdn.microsoft.com/zh-tw/library/ms679635(v=vs.85).aspx)
    3. value 則填上使用者ad帳號
    4. 按下 add 新增條件
    5. 按下 search 查詢結果

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170201/0003.png" alt="0003"/>
    > 可用滑鼠在查出結果點兩下可以瀏覽相關資料

## RocketChat LADP 
1. 先看 [logon with username](https://rocket.chat/docs/administrator-guides/authentication/ldap#logon-with-username-) 相關設定

2. 再用 AdExplorer 查出 Dn (distinguishedName)

    ```
    DC=yyy,dc=zzz
    ```
    
    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170201/0004.png" alt="0004"/>
3. 再開RocketChat LDAP配置填至Domain Base 欄位

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170201/0005.png" alt="0005"/>
4. 最後再填上登入帳密查詢User AD

    <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170201/0006.png" alt="0006"/>

## 參考資料
- [RocketChat LDAP](https://rocket.chat/docs/administrator-guides/authentication/ldap/)
- [wiki](https://zh.wikipedia.org/wiki/Active_Directory)
- [LDAP 基礎說明](http://blog.xuite.net/tolarku/blog/151029105-LDAP+%E5%9F%BA%E7%A4%8E%E8%AA%AA%E6%98%8E)