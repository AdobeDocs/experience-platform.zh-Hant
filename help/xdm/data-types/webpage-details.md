---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；網頁詳細資訊；資料型別；資料型別；網頁
solution: Experience Platform
title: 網頁詳細資料資料型別
description: 瞭解網頁詳細資訊Experience Data Model (XDM)資料型別。
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 11%

---

# [!UICONTROL 網頁詳細資料]資料型別

[!UICONTROL 網頁詳細資料]是標準的Experience Data Model (XDM)資料型別，描述剛剛載入及檢視之網頁的詳細資料，如ExperienceEvent所記錄。

此資料型別適用於單頁網頁應用程式(SPA)的完整頁面詳細資料和初始頁面載入。 若為載入頁面上發生的互動不會觸發新頁面載入，請參閱[網頁互動](./web-interaction.md)資料型別。

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL 量值]](./measure.md) | 網頁的檢視次數。 |
| `URL` | 字串 | 網頁的規範或一般URL。 這可能是也可能不是用來存取頁面的實際URL。 若要記錄用來存取網頁的URL，請使用`webLink`。 URI格式應該遵循[RFC 3986](https://tools.ietf.org/html/rfc3986)標準。 |
| `isErrorPage` | 布林值 | 此屬性使用旗標來指示頁面是否為錯誤頁面。 此標幟可用來將網頁互動廣泛分類。 錯誤由應用程式定義，並可對應至提供HTTP錯誤碼的頁面。 |
| `isHomePage` | 布林值 | 此屬性使用旗標來指示頁面是否為首頁。 此標幟可用來將網頁互動廣泛分類。 首頁的定義由應用程式決定。 |
| `name` | 字串 | 網頁的規範名稱。這個名稱不必然是網頁標題或和頁面內容直接相關，但用於編排網站頁面，達到分類目的。 |
| `server` | 字串 | 代管網頁的規範或一般伺服器。 這有可能是也可能不是實際提供頁面互動的主機或伺服器。 |
| `siteSection` | 字串 | 此網頁所在的網站區段的規範名稱。 這可用來將互動分類或歸類。 |
| `viewName` | 字串 | 頁面中檢視的名稱。 此屬性常用於具有變更大部分頁面版面的索引標籤或控制項的單頁應用程式或頁面。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
