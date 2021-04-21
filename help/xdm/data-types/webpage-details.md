---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；Schemas;Webpage details;datatype;data type;webpage
solution: Experience Platform
title: 網頁詳細資料資料類型
topic-legacy: overview
description: 本檔案提供網頁詳細資訊「體驗資料模型」(XDM)資料類型的概觀。
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 2%

---

# [!UICONTROL Web page details] 資料類型

[!UICONTROL Web page details] 是標準的「體驗資料模型」(XDM)資料類型，說明ExperienceEvent所記錄之剛載入及檢視之網頁的詳細資訊。

資料類型適用於單頁網頁應用程式(SPA)的完整頁面詳細資訊和初始頁面載入。 如需在載入頁面上發生的互動，而未觸發新頁面載入，請參閱[網頁互動](./web-interactions.md)資料類型。

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Measure]](./measure.md) | 網頁上的檢視次數。 |
| `URL` | 字串 | 網頁的規範或一般URL。 這可能是用來到達頁面的實際URL，也可能不是。 若要記錄用來到達頁面的URL，請使用`webLink`。 URI格式應遵循[RFC 3986](https://tools.ietf.org/html/rfc3986)標準。 |
| `isErrorPage` | 布林值 | 此屬性使用標幟來指出頁面是否為錯誤頁面。 此標幟可用來廣泛分類網頁互動。 錯誤由應用程式定義，並可對應至以HTTP錯誤碼提供的頁面。 |
| `isHomePage` | 布林值 | 此屬性使用標幟來指出頁面是否為首頁。 此標幟可用來廣泛分類網頁互動。 首頁的定義由應用程式決定。 |
| `name` | 字串 | 網頁的規範性名稱。 此名稱不一定是頁面標題或直接與頁面內容關聯，但用於組織網站的頁面以利分類。 |
| `server` | 字串 | 代管網頁的規範或一般伺服器。 這可能是實際提供頁面互動功能的主機或伺服器，也可能不是。 |
| `siteSection` | 字串 | 此網頁所在網站區域的規範性名稱。 這可用來分類或分類互動。 |
| `viewName` | 字串 | 頁面內的檢視名稱。 此屬性通常用於具有可變更大部分頁面版面的標籤或控制項的單頁應用程式或頁面。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.example.2.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.schema.json)
