---
title: 開發擴充功能
description: 本檔案提供標籤擴充功能開發程式的一般概覽，以及進一步說明檔案的連結，以取得更詳細的程式。
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: cfcc70d66a34fa51bf0e21525539ba88de7fc367
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 31%

---

# 開發擴充功能

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

標籤擴充功能應視為具有自身需求的（小型）產品。 判斷Adobe Experience Platform使用者將如何使用您的擴充功能，可協助您將功能分類為您的擴充功能所應提供的事件型別、條件型別、動作型別和資料元素型別。

有了這些知識，您就可以規劃應在擴充功能中提供哪些元件。

## 指南

計畫就緒後，這些指南將可協助您了解擴充功能的開發流程：

* 左側導覽中的[快速入門手冊](../getting-started.md)和位於&#x200B;**擴充功能開發**&#x200B;下的其他檔案，是瞭解擴充功能的絕佳參考資料。 其中包含擴充功能的功能、如何儲存使用者資訊以及在擴充功能與Adobe Experience Platform之間加以傳遞、如何將程式碼整合至程式庫中，以及在執行階段如何在瀏覽器中解譯和使用擴充功能程式碼的詳細資訊。
<!-- * The [extension tutorial video](https://youtu.be/rxjtC9o4rl0) is a great place to start. -->
* [擴充功能簡介](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube 播放清單會逐步說明建立擴充功能套件的程序。
* [了解 JSON 結構描述](https://spacetelescope.github.io/understanding-json-schema/index.html#)文章。
* [JSON Lint/驗證器](https://jsonlint.com/)。
* [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Chrome 擴充功能可醒目提示及列印 JSON 和 JSONP。
* [jsonschema.net](https://jsonschema.net/#/editor)編輯器可協助您從物件建立JSON結構描述。
* [JSON Schema Validator](https://www.jsonschemavalidator.net)：一款線上互動式 JSON 結構描述驗證器。

## 工具

此外，還有許多 npm 工具可協助您進行擴充功能套件開發：

* [標籤延伸架構工具](https://www.npmjs.com/package/@adobe/reactor-scaffold)可協助您在本機電腦上輕鬆建立入門專案。
* [標籤擴充功能沙箱](https://www.npmjs.com/package/@adobe/reactor-sandbox)可協助您驗證本機電腦上的擴充功能檢視和模組。
* [Tag Extension Packager](https://www.npmjs.com/package/@adobe/reactor-packager)是一個命令列公用程式，用於將標籤延伸封裝成zip檔案。
* [Tag Extension Uploader](https://www.npmjs.com/package/@adobe/reactor-uploader)是互動式命令列工具，可協助您輸入技術帳戶認證，並將擴充功能套件上傳至標籤。
* [Tag Extension Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser)是互動式命令列工具，可協助您發行擴充功能以供私人使用。

## 範例擴充功能

GitHub上有範例擴充功能，可供檢閱或作為起始專案：

* [Hello World 範例擴充功能](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook 範例擴充功能](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit 範例擴充功能](https://github.com/jeffchasin/extension-typekit)
* [Pinterest 範例擴充功能](https://github.com/jeffchasin/extension-pinterest)

## Slack 工作區

您可以要求存取Slack社群工作區，擴充功能作者可使用此[要求表單](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform)互相支援。

**請注意**：雖然此Slack工作區中有Adobe的成員，但這項社群資源並非由Adobe贊助或主導。
