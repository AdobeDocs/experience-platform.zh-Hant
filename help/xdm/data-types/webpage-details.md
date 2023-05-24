---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；模式；網頁詳細資訊；資料類型；資料類型；網頁
solution: Experience Platform
title: 網頁詳細資訊資料類型
description: 本文檔提供網頁詳細資訊體驗資料模型(XDM)資料類型的概述。
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# [!UICONTROL 網頁詳細資訊] 資料類型

[!UICONTROL 網頁詳細資訊] 是標準的體驗資料模型(XDM)資料類型，它描述由ExperienceEvent記錄的有關剛剛載入和查看的網頁的詳細資訊。

資料類型用於單頁Web應用程式(SPA)的完整頁詳細資訊和初始頁載入。 有關在未觸發新頁面載入的載入頁面上發生的交互，請參見 [Web交互](./web-interaction.md) 資料類型。

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL 度量]](./measure.md) | 網頁上的視圖數。 |
| `URL` | 字串 | 網頁的規範或常規URL。 這可能是或不是用於訪問頁面的實際URL。 記錄用於訪問頁面使用的URL `webLink`。 URI格式應跟在 [RFC 3986](https://tools.ietf.org/html/rfc3986) 標準。 |
| `isErrorPage` | 布林值 | 此屬性使用標誌來指示該頁是否為錯誤頁。 此標誌用於對Web交互進行廣泛分類。 該錯誤由應用程式定義，並且可以與帶有HTTP錯誤代碼的頁面對應。 |
| `isHomePage` | 布林值 | 此屬性使用標誌來指示該頁是否是首頁。 此標誌用於對Web交互進行廣泛分類。 首頁的定義由應用程式確定。 |
| `name` | 字串 | 網頁的規範名稱。 此名稱不一定是頁面標題或直接與頁面內容關聯，但用於組織網站的頁面以用於分類。 |
| `server` | 字串 | 承載網頁的規範伺服器或常規伺服器。 這可能是實際為頁面交互服務的主機或伺服器。 |
| `siteSection` | 字串 | 此網頁所在站點節的規範名稱。 這可用於對交互進行分類或分類。 |
| `viewName` | 字串 | 頁面內視圖的名稱。 此屬性通常用於具有更改大部分頁面佈局的頁籤或控制項的單頁應用程式或頁面。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
