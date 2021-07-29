---
title: 開發擴充功能
description: 本檔案提供標籤擴充功能開發程式的一般概述，其中提供進一步檔案的連結，以取得更詳細的程式。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 39%

---

# 開發擴充功能

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

標籤擴充功能應視為具有自身需求的（小型）產品。 判斷 Adobe Experience Platform 使用者將如何使用您的擴充功能，可協助您將功能分類為您的擴充功能所應提供的事件類型、條件類型、動作類型和資料元素類型。

有了這些知識，您就可以規劃應在擴充功能中提供哪些元件。

## 指南

計畫就緒後，這些指南將可協助您了解擴充功能的開發流程：

* [快速入門手冊](../getting-started.md)和左側導覽中&#x200B;**擴充功能開發**&#x200B;下的其他檔案，是了解擴充功能的絕佳參考資料。 其中包括擴充功能的功能、如何儲存使用者資訊並在擴充功能與Adobe Experience Platform之間傳遞、如何將程式碼整合至程式庫，以及在瀏覽器的執行階段如何解譯和使用您的擴充功能程式碼的詳細資訊。
* [擴充功能教學課程影片](https://youtu.be/rxjtC9o4rl0)是絕佳的起點。
* [擴充功能簡介](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube 播放清單會逐步說明建立擴充功能套件的程序。
* [了解 JSON 結構描述](https://spacetelescope.github.io/understanding-json-schema/index.html#)文章。
* [JSON Lint/Validator](http://jsonlint.com/)。
* [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Chrome 擴充功能可醒目提示及列印 JSON 和 JSONP。
* [jsonschema.net](https://jsonschema.net/#/editor) 編輯器可協助您從物件建立 JSON 結構描述。
* [JSON Schema Validator](http://www.jsonschemavalidator.net/)：一款線上互動式 JSON 結構描述驗證器。

## 工具

此外，還有許多 npm 工具可協助您進行擴充功能套件開發：

* [標籤擴充功能架](https://www.npmjs.com/package/@adobe/reactor-scaffold) 構工具可協助您在本機電腦上輕鬆建立入門專案。
* [標籤擴充](https://www.npmjs.com/package/@adobe/reactor-sandbox) 功能沙箱可協助您驗證本機電腦上的擴充功能檢視和模組。
* [Tag Extension Packager](https://www.npmjs.com/package/@adobe/reactor-packager) 是命令列公用程式，可將標籤副檔名封裝成zip檔案。
* [Tag Extension Uploader是](https://www.npmjs.com/package/@adobe/reactor-uploader) 一個互動式命令列工具，可協助您輸入技術帳戶認證，並將擴充功能套件上傳至標籤。
* [Tag Extension Releaser是](https://www.npmjs.com/package/@adobe/reactor-releaser) 互動式命令列工具，可協助您發行擴充功能供私人使用。

## 範例擴充功能

GitHub上有範例擴充功能，您可以檢閱或作為入門專案：

* [Hello World 範例擴充功能](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook 範例擴充功能](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit 範例擴充功能](https://github.com/jeffchasin/extension-typekit)
* [Pinterest 範例擴充功能](https://github.com/jeffchasin/extension-pinterest)

## Slack 工作區

您可以透過此[要求表單](http://join.launchdevelopers.chat)，要求存取Slack社群工作區，供擴充功能作者相互支援。

**請注意**:雖然此Slack工作區中有Adobe的成員，但這是社群資源，並非由Adobe贊助或主導。
