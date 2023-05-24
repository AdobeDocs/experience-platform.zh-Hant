---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；瀏覽器；瀏覽器詳細資訊；資料類型；資料類型；資料類型；
solution: Experience Platform
title: 瀏覽器詳細資訊資料類型
description: 此文檔概述了「瀏覽器詳細資訊」XDM資料類型。
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 11%

---

# [!UICONTROL 瀏覽器詳細資訊] 資料類型

[!UICONTROL 瀏覽器詳細資訊] 是標準XDM資料類型，它描述與瀏覽器或應用程式相關的詳細資訊。

<img src="../images/data-types/browser-details.png" width="450" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `acceptLanguage` | 字串 | IETF語言標籤([RFC 5646](https://tools.ietf.org/html/rfc5646))。 |
| `cookiesEnabled` | 布林值 | 指示用戶的設定是否允許寫入Cookie。 |
| `javaEnabled` | 布林值 | 指示是否在從中進行觀察的設備中啟用了Java。 |
| `javaScriptEnabled` | 布林值 | 指示是否在從中進行觀察的設備中啟用了JavaScript。 |
| `javaScriptVersion` | 字串 | 觀察期間支援的JavaScript版本。 |
| `javaVersion` | 字串 | 觀察期間支援的Java版本。 |
| `name` | 字串 | 應用程式或瀏覽器名稱。 |
| `quicktimeVersion` | 字串 | 觀察期間支援的AppleQuicktime版本。 |
| `thirdPartyCookiesEnabled` | 布林值 | 指示是否在觀察所依據的設備中啟用了第三方Cookie。 |
| `userAgent` | 字串 | 客戶端請求中的HTTP用戶代理字串。 |
| `vendor` | 字串 | 應用程式或瀏覽器供應商。 |
| `version` | 字串 | 應用程式或瀏覽器版本。 |
| `viewportHeight` | 整數 | 事件顯示在內部的窗口的垂直大小（像素）。 對於Web視圖事件，這是瀏覽器視區高度。 |
| `viewportWidth` | 整數 | 事件顯示在內部的窗口的水準大小（像素）。 對於Web視圖事件，這是瀏覽器視區寬度。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
