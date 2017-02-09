---
layout: post
category : article
title : Visual Studio 2013 Extension File Nesting add Typescript Rule (記錄)
---

## 簡述

在 [VSCommands](https://marketplace.visualstudio.com/items?itemName=SquaredInfinityJarekKardas.VSCommandsforVisualStudio2013){:target="_blank"} 有個 Group Items的功能，可以把Typescript 產出的js Group起來，但需要單一操作，於是找到 [File Nesting](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.FileNesting){:target="_blank"} 擴充套件，可快速將專案檔案按照規則一次性Group，但作者目前版本已不支援vs2013及Typescript規則(需自訂)，因此個人做了以下修正及記錄。

## VS2013 環境準備

- 請先下載 [VS2013 SDK](https://www.microsoft.com/en-us/download/details.aspx?id=40758){:target="_blank"}
- 原套件Github位置：[FileNesting](https://github.com/madskristensen/FileNesting){:target="_blank"}
- 若vs2013請用git clone的方式下載，再切換到5/20的Commit記錄做修改。
- 主要修改內容：
  1. [src\Dialogs\NestingOptions.cs](https://github.com/leejulee/FileNesting/blob/VS2013_TypeScript/src/Dialogs/NestingOptions.cs){:target="_blank"} (增加 EnableTypescriptRule 屬性)
  2. [src\Nesters\Automated\TypescriptNester.cs](https://github.com/leejulee/FileNesting/blob/VS2013_TypeScript/src/Nesters/Automated/TypescriptNester.cs){:target="_blank"} (新增 TypeScript 規則的 TypescriptNester.cs)
  3. [src\Nesters\FileNestingFactory](https://github.com/leejulee/FileNesting/blob/VS2013_TypeScript/src/Nesters/FileNestingFactory.cs){:target="_blank"} (新增 TypescriptNester 項目)
- [詳細異動記錄](https://github.com/leejulee/FileNesting/commit/502f72f8a775293a0f4686c1fe174460b143f9cd){:target="_blank"}
- 修改後Github位置：[https://github.com/leejulee/FileNesting/tree/VS2013_TypeScript](https://github.com/leejulee/FileNesting/tree/VS2013_TypeScript){:target="_blank"}

## VS2013 設定配置
- ### Tools→Options (設置開啟Typescript Rule)
  ![001]({{ site.url }}/assets/images/posts/20160604/001.png "001")
- ### 在最上層資料夾鍵右鍵→File Nesting → Auto-nest selected items 
  ![002]({{ site.url }}/assets/images/posts/20160604/002.png "002")
- ### 成功結果
  ![003]({{ site.url }}/assets/images/posts/20160604/003.png "003")

### 參考資料
[Extension Debug](http://stackoverflow.com/questions/9281662/how-to-debug-visual-studio-extensions){:target="_blank"}