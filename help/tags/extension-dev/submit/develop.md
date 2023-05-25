---
title: 開發擴充功能
description: 本檔案提供標籤擴充功能開發程式的一般概覽，以及更多詳細程式的進一步檔案連結。
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 43%

---

# 開發擴充功能

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

標籤擴充功能應視為具有自身需求的（小型）產品。 判斷 Adobe Experience Platform 使用者將如何使用您的擴充功能，可協助您將功能分類為您的擴充功能所應提供的事件類型、條件類型、動作類型和資料元素類型。

有了這些知識，您就可以規劃擴充功能中應該提供哪些元件。

## 指南

計畫就緒後，這些指南將可協助您了解擴充功能的開發流程：

* 此 [快速入門手冊](../getting-started.md) 下的其他檔案 **擴充功能開發** 左側導覽中的「 」是瞭解擴充功能的絕佳參考資料。 其中包含擴充功能的功能、如何儲存使用者資訊以及在擴充功能和Adobe Experience Platform之間加以傳遞、如何將程式碼整合到程式庫中，以及在執行階段如何在瀏覽器中解譯和使用擴充功能程式碼的詳細資訊。
* 此 [擴充功能教學課程影片](https://youtu.be/rxjtC9o4rl0) 是個絕佳的起點。
* [擴充功能簡介](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube 播放清單會逐步說明建立擴充功能套件的程序。
* [了解 JSON 結構描述](https://spacetelescope.github.io/understanding-json-schema/index.html#)文章。
* [JSON Lint/Validator](https://jsonlint.com/)。
* [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Chrome 擴充功能可醒目提示及列印 JSON 和 JSONP。
* [jsonschema.net](https://jsonschema.net/#/editor) 編輯器可協助您從物件建立 JSON 結構描述。
* [JSON Schema Validator](https://www.jsonschemavalidator.net)：一款線上互動式 JSON 結構描述驗證器。

## 工具

此外，還有許多 npm 工具可協助您進行擴充功能套件開發：

* [標籤延伸架構工具](https://www.npmjs.com/package/@adobe/reactor-scaffold) 可協助您在本機電腦上輕鬆建立入門專案。
* [標籤延伸模組沙箱](https://www.npmjs.com/package/@adobe/reactor-sandbox) 可協助您驗證本機電腦上的擴充功能檢視和模組。
* [標籤延伸封裝程式](https://www.npmjs.com/package/@adobe/reactor-packager) 是一個命令列公用程式，用於將標籤副檔名封裝到zip檔案中。
* [標籤延伸上傳程式](https://www.npmjs.com/package/@adobe/reactor-uploader) 是一款互動式命令列工具，可協助您輸入技術帳戶認證，並將擴充功能套件上傳至標籤。
* [標籤延伸功能發行者](https://www.npmjs.com/package/@adobe/reactor-releaser) 是一款互動式命令列工具，可協助您發行擴充功能供私人使用。

## 範例擴充功能

GitHub上有範例擴充功能，可供檢閱或作為起始專案：

* [Hello World 範例擴充功能](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook 範例擴充功能](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit 範例擴充功能](https://github.com/jeffchasin/extension-typekit)
* [Pinterest 範例擴充功能](https://github.com/jeffchasin/extension-pinterest)

## Slack 工作區

您可以要求Slack社群工作區的存取權，擴充功能作者可透過此工具互相支援 [請求表單](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**請注意**：雖然此Slack工作區中有Adobe的成員，但這項社群資源並非由Adobe贊助或主導。
