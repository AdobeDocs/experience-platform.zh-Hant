---
keywords: Experience Platform;home；常用主題；模式；模式；XDM;fields；模式；瀏覽器；瀏覽器詳細資訊；資料類型；資料類型；
solution: Experience Platform
title: 瀏覽器詳細資料資料類型
topic-legacy: overview
description: 本文檔概述了「瀏覽器詳細資訊」XDM資料類型。
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 6%

---

# [!UICONTROL Browser details] 資料類型

[!UICONTROL Browser details] 是標準的XDM資料類型，可說明與瀏覽器或應用程式相關的詳細資訊。

<img src="../images/data-types/browser-details.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `acceptLanguage` | 字串 | IETF語言標籤([RFC 5646](https://tools.ietf.org/html/rfc5646))。 |
| `cookiesEnabled` | 布林值 | 指出使用者的設定是否允許編寫Cookie。 |
| `javaEnabled` | 布林值 | 指出是否在觀察所依據的裝置中啟用Java。 |
| `javaScriptEnabled` | 布林值 | 指出是否在觀察所依據的裝置中啟用JavaScript。 |
| `javaScriptVersion` | 字串 | 觀察期間支援的JavaScript版本。 |
| `javaVersion` | 字串 | 觀察期間支援的Java版本。 |
| `name` | 字串 | 應用程式或瀏覽器名稱。 |
| `quicktimeVersion` | 字串 | 觀察期間支援的Apple Quicktime版本。 |
| `thirdPartyCookiesEnabled` | 布林值 | 指出是否在觀察所依據的裝置中啟用第三方Cookie。 |
| `userAgent` | 字串 | 來自用戶端請求的HTTP user-agent字串。 |
| `vendor` | 字串 | 應用程式或瀏覽器廠商。 |
| `version` | 字串 | 應用程式或瀏覽器版本。 |
| `viewportHeight` | 整數 | 事件顯示於視窗內的垂直大小（像素）。 對於Web檢視事件，此為瀏覽器檢視區高度。 |
| `viewportWidth` | 整數 | 事件顯示於其中之視窗的水準大小（像素）。 對於Web檢視事件，此為瀏覽器檢視埠寬度。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
