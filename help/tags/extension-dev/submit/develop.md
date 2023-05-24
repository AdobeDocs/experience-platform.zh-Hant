---
title: 開發擴展
description: 本文檔提供標籤擴展開發過程的一般概述，並提供指向更詳細流程的進一步文檔的連結。
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 43%

---

# 開發擴充功能

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

標籤擴展應被視為具有自身要求的（小）產品。 判斷 Adobe Experience Platform 使用者將如何使用您的擴充功能，可協助您將功能分類為您的擴充功能所應提供的事件類型、條件類型、動作類型和資料元素類型。

借助這些知識，您可以規劃在擴展中應提供哪些元件。

## 指南

計畫就緒後，這些指南將可協助您了解擴充功能的開發流程：

* 的 [入門指南](../getting-started.md) 及其他檔案 **擴展開發** 在左側導航中，是瞭解擴展的極好參考材料。 它們包括以下詳細資訊：擴展功能可以做什麼，擴展和Adobe Experience Platform之間如何儲存和傳遞用戶資訊，如何將代碼捆綁到庫中，以及在瀏覽器運行時如何解釋和使用擴展代碼。
* 的 [擴展教程視頻](https://youtu.be/rxjtC9o4rl0) 是個很好的起點。
* [擴充功能簡介](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube 播放清單會逐步說明建立擴充功能套件的程序。
* [了解 JSON 結構描述](https://spacetelescope.github.io/understanding-json-schema/index.html#)文章。
* [JSON Lint/Validator](https://jsonlint.com/)。
* [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Chrome 擴充功能可醒目提示及列印 JSON 和 JSONP。
* [jsonschema.net](https://jsonschema.net/#/editor) 編輯器可協助您從物件建立 JSON 結構描述。
* [JSON Schema Validator](https://www.jsonschemavalidator.net)：一款線上互動式 JSON 結構描述驗證器。

## 工具

此外，還有許多 npm 工具可協助您進行擴充功能套件開發：

* [標籤擴展支架工具](https://www.npmjs.com/package/@adobe/reactor-scaffold) 幫助您輕鬆在本地電腦上建立啟動程式項目。
* [標籤擴展沙盒](https://www.npmjs.com/package/@adobe/reactor-sandbox) 幫助您驗證本地電腦上的擴展視圖和模組。
* [標籤擴展打包器](https://www.npmjs.com/package/@adobe/reactor-packager) 是命令行實用程式，用於將標籤副檔名打包到zip檔案中。
* [標籤擴展上載程式](https://www.npmjs.com/package/@adobe/reactor-uploader) 是互動式命令行工具，可幫助您輸入技術帳戶憑據並將擴展包上載到標籤。
* [標籤擴展釋放器](https://www.npmjs.com/package/@adobe/reactor-releaser) 是互動式命令行工具，可幫助您釋放擴展到私有可用性。

## 範例擴充功能

GitHub上有一些擴展示例，您可以查看或用作啟動項目：

* [Hello World 範例擴充功能](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook 範例擴充功能](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit 範例擴充功能](https://github.com/jeffchasin/extension-typekit)
* [Pinterest 範例擴充功能](https://github.com/jeffchasin/extension-pinterest)

## Slack 工作區

您可以請求訪問Slack社區工作區，擴展作者可在此工作區中相互支援 [申請表](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform)。

**請注意**:雖然此Adobe工作區中有Slack成員，但它是社區資源，不由Adobe贊助或監督。
