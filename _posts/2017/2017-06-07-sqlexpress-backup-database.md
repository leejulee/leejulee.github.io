---
layout: post
category : article
title : SQL Express Backup Database
tags : [SQL]
---

## 環境
- SQL Expresss (starting with 2008)
- sqlcmd

## 事先閱讀
- [How to schedule and automate backups of SQL Server databases in SQL Server Express](https://support.microsoft.com/en-us/help/2019698/how-to-schedule-and-automate-backups-of-sql-server-databases-in-sql-server-express)
- [sqlcmd](https://msdn.microsoft.com/zh-tw/library/ms180944.aspx)

## 操作步驟

- create backupSQL file

    ```
    PRINT '==============================Start=========================================='
    PRINT ''

    USE [master] 
    GO 

    SET ANSI_NULLS ON 
    GO 
    SET QUOTED_IDENTIFIER ON 
    GO 
    
    DECLARE 
    @DB_NAME VARCHAR(128) = N'leodb',
    @BACKUP_PATH VARCHAR(64) = N'D:\downloadTemp\dbbackup',
    --datetime format https://www.w3schools.com/sql/func_convert.asp
    @DateTime NVARCHAR(20)  = REPLACE(CONVERT(VARCHAR, GETDATE(),102),'.','') 
                                + '__' +  REPLACE(CONVERT(VARCHAR, GETDATE(),108),':',''),
    @BackupName varchar(100)
        
    SET @BACKUP_PATH = @BACKUP_PATH + '\' + @dateTime + '_' + @DB_NAME + '.bak'

    PRINT @BACKUP_PATH

    --Backing Up a Whole Database   
    BACKUP DATABASE [leodb]
    TO DISK = @BACKUP_PATH
    WITH INIT --是否初始化備份覆寫已存在檔案(INIT)或是附加已存在檔案上(預設NOINIT)

    PRINT ''
    PRINT '==============================END============================================'
    ```

- create batch file

    - `-i` 是讀取檔案輸入指令、`-o` 檔案輸出指令

    ```
    sqlcmd -i C:\MyFolder\MyScript.sql -o C:\MyFolder\MyOutput_log.txt
    ```

- create 工作排程

    - 打開工作排程

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170607/0001.png" alt="0001"/>

    - 建立基本工作任務

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170607/0002.png" alt="0002"/>

    - 選擇執行方式 (天、週、月......)

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170607/0003.png" alt="0003"/>
    
    - 選擇執行時間

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170607/0004.png" alt="0004"/>

    - 選擇動作為執行程式 (execute batch file)

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170607/0005.png" alt="0005"/>

    - 選擇程式檔案路徑 (batch file)

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170607/0006.png" alt="0006"/>

    - 選擇確認完成建立

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170607/0007.png" alt="0007"/>

    - 排程列表

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170607/0008.png" alt="0008"/>

- 執行結果

    - 執行完成後的檔案列表，多兩個檔案 (db bak、log檔)

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170607/0009.png" alt="0009"/>

    - 執行完成後的log檔內容

        <img class="img-responsive" src="{{ site.url }}/assets/images/posts/20170607/0010.png" alt="0010"/>