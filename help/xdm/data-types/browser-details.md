---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；瀏覽器；瀏覽器詳細資訊；資料型別；資料型別；
solution: Experience Platform
title: 瀏覽器詳細資料型別
description: 瞭解瀏覽器詳細資料XDM資料型別。
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 27%

---

# [!UICONTROL 瀏覽器詳細資料]資料型別

[!UICONTROL 瀏覽器詳細資料]是標準的XDM資料型別，說明與瀏覽器或應用程式相關的詳細資料。

![](../images/data-types/browser-details.png){width=450}

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `acceptLanguage` | 字串 | IETF語言標籤([RFC 5646](https://tools.ietf.org/html/rfc5646))。 |
| `cookiesEnabled` | 布林值 | 指出使用者的設定是否允許寫入Cookie。 |
| `javaEnabled` | 布林值 | 表示進行觀察的裝置是否已啟用Java。 |
| `javaScriptEnabled` | 布林值 | 表示進行觀察的裝置是否已啟用JavaScript。 |
| `javaScriptVersion` | 字串 | 在觀察期間受支援的 JavaScript 版本。 |
| `javaVersion` | 字串 | 在觀察期間受支援的 Java 版本。 |
| `name` | 字串 | 應用程式或瀏覽器名稱。 |
| `quicktimeVersion` | 字串 | 在觀察期間受支援的 Apple Quicktime 版本。 |
| `thirdPartyCookiesEnabled` | 布林值 | 指出進行觀察的裝置是否已啟用第三方Cookie。 |
| `userAgent` | 字串 | 來自用戶端請求的 HTTP 使用者代理字串。 |
| `vendor` | 字串 | 應用程式或瀏覽器供應商。 |
| `version` | 字串 | 應用程式或瀏覽器版本。 |
| `viewportHeight` | 整數 | 顯示事件之視窗的垂直大小（畫素）。 若為網頁檢視事件，此為瀏覽器檢視區高度。 |
| `viewportWidth` | 整數 | 顯示事件之視窗的水準大小（畫素）。 若為網頁檢視事件，此為瀏覽器檢視區寬度。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
