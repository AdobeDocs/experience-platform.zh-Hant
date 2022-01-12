---
title: 開發擴充功能
description: 本檔案提供標籤擴充功能開發程式的一般概述，其中提供進一步檔案的連結，以取得更詳細的程式。
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 43%

---

# 開發擴充功能

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

標籤擴充功能應視為具有自身需求的（小型）產品。 判斷 Adobe Experience Platform 使用者將如何使用您的擴充功能，可協助您將功能分類為您的擴充功能所應提供的事件類型、條件類型、動作類型和資料元素類型。

有了這些知識，您就可以規劃應在擴充功能中提供哪些元件。

## 指南

計畫就緒後，這些指南將可協助您了解擴充功能的開發流程：

* 此 [快速入門手冊](../getting-started.md) 和其他檔案 **擴充功能開發** 在左側導覽中，提供絕佳的參考資料，方便您了解擴充功能。 其中包含擴充功能的功能、如何儲存使用者資訊並在擴充功能與Adobe Experience Platform之間傳遞、如何將程式碼整合至程式庫，以及在瀏覽器執行階段如何解譯和使用您的擴充功能程式碼的詳細資訊。
* 此 [擴充功能教學課程影片](https://youtu.be/rxjtC9o4rl0) 是一個絕佳的起點。
* [擴充功能簡介](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube 播放清單會逐步說明建立擴充功能套件的程序。
* [了解 JSON 結構描述](https://spacetelescope.github.io/understanding-json-schema/index.html#)文章。
* [JSON Lint/Validator](https://jsonlint.com/)。
* [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Chrome 擴充功能可醒目提示及列印 JSON 和 JSONP。
* [jsonschema.net](https://jsonschema.net/#/editor) 編輯器可協助您從物件建立 JSON 結構描述。
* [JSON Schema Validator](https://www.jsonschemavalidator.net)：一款線上互動式 JSON 結構描述驗證器。

## 工具

此外，還有許多 npm 工具可協助您進行擴充功能套件開發：

* [標籤擴充功能架構工具](https://www.npmjs.com/package/@adobe/reactor-scaffold) 可協助您在本機電腦上輕鬆建立入門專案。
* [標籤擴充功能沙箱](https://www.npmjs.com/package/@adobe/reactor-sandbox) 可協助您驗證本機電腦上的擴充功能檢視和模組。
* [Tag Extension Packager](https://www.npmjs.com/package/@adobe/reactor-packager) 是命令列公用程式，可將標籤副檔名封裝成zip檔案。
* [標籤擴充功能上傳程式](https://www.npmjs.com/package/@adobe/reactor-uploader) 是互動式命令列工具，可協助您輸入技術帳戶認證，並將擴充功能套件上傳至標籤。
* [Tag Extension Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser) 是互動式命令列工具，可協助您發行擴充功能供私人使用。

## 範例擴充功能

GitHub上有範例擴充功能，您可以檢閱或作為入門專案：

* [Hello World 範例擴充功能](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook 範例擴充功能](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit 範例擴充功能](https://github.com/jeffchasin/extension-typekit)
* [Pinterest 範例擴充功能](https://github.com/jeffchasin/extension-pinterest)

## Slack 工作區

您可以要求存取Slack社群工作區，擴充功能作者可透過此支援彼此 [申請表](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**請注意**:雖然此Slack工作區中有Adobe的成員，但這是社群資源，並非由Adobe贊助或主導。
