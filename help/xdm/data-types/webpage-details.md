---
keywords: Experience Platform；首頁；熱門主題；方案；方案； XDM；欄位；方案；方案；網頁詳細資訊；資料類型；資料類型；網頁
solution: Experience Platform
title: 網頁詳細資料資料類型
topic-legacy: overview
description: 本檔案概述網頁詳細資訊Experience Data Model(XDM)資料類型。
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 3%

---

# [!UICONTROL 網頁詳細資] 料資料類型

[!UICONTROL 網頁詳] 細資訊是標準的Experience Data Model(XDM)資料類型，可說明剛載入並檢視之網頁的詳細資訊（由ExperienceEvent記錄）。

資料類型適用於單頁Web應用程式(SPA)的完整頁面詳細資料和初始頁面載入。 對於在載入頁面上發生的未觸發新頁面載入的互動，請參閱[web互動](./web-interaction.md)資料類型。

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL 測量]](./measure.md) | 網頁上的檢視次數。 |
| `URL` | 字串 | 網頁的規範或一般URL。 這可能是或不是用來存取頁面的實際URL。 若要記錄用來存取頁面的URL，請使用`webLink`。 URI格式應遵循[RFC 3986](https://tools.ietf.org/html/rfc3986)標準。 |
| `isErrorPage` | 布林值 | 此屬性會使用標幟來指出頁面是否為錯誤頁面。 此標幟可廣泛分類網路互動。 錯誤由應用程式定義，並可對應至提供HTTP錯誤碼的頁面。 |
| `isHomePage` | 布林值 | 此屬性會使用標幟來指出頁面是否為首頁。 此標幟可廣泛分類網路互動。 首頁的定義由應用程式決定。 |
| `name` | 字串 | 網頁的規範性名稱。 此名稱不一定是頁面標題或與頁面內容直接關聯，而是用來組織網站的頁面以用於分類。 |
| `server` | 字串 | 承載網頁的規範或一般伺服器。 這可能是或不是實際提供頁面互動的主機或伺服器。 |
| `siteSection` | 字串 | 此網頁所在網站區域的規範性名稱。 這可用來分類互動或加以分類。 |
| `viewName` | 字串 | 頁面內的檢視名稱。 此屬性通常用於單頁應用程式或具有可更改大多數頁面佈局的標籤或控制項的頁面。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
