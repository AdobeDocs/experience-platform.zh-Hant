---
title: 自動收集的資訊
description: Adobe Experience Platform Web SDK自動收集的資料概觀。
source-git-commit: 89b981104e3cbe597d1556484f4365866bf2a11d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 2%

---

# 自動收集的資訊

Adobe Experience Platform Web SDK會自動收集一些立即可用的資訊。 如果您的組織不想自動收集此資料，您可以使用 `context` 中的選項 [`configure` 命令](../fundamentals/configuring-the-sdk.md).

從排除的關鍵字 `context` 資料收集中未包含陣列。 如果 `context` 陣列不存在於 `configure` 指令，則會自動收集下表中的所有資料。

| 名稱 | 說明 | `context` 陣列關鍵字 | XDM 路徑 | 範例值 |
| --- | --- | --- | --- | --- |
| 熒幕高度 | 熒幕的高度（畫素）。 | `device` | `events[].xdm.device.screenHeight` | `900` |
| 熒幕寬度 | 熒幕的寬度（畫素）。 | `device` | `events[].xdm.device.screenWidth` | `1440` |
| 熒幕方向 | 熒幕方向。 | `device` | `events[].xdm.device.screenOrientation` | `landscape` 或 `portrait` |
| 環境類型 | 體驗出現的環境型別。 Adobe Experience Platform Web SDK一律會將此欄位設為 `browser`. | `environment` | `events[].xdm.environment.type` | `browser` |
| 檢視區高度 | 瀏覽器內容區域的高度（畫素）。 | `environment` | `events[].xdm.environment.browserDetails.viewportHeight` | `679` |
| 檢視區寬度 | 瀏覽器內容區域的寬度（畫素）。 | `environment` | `events[].xdm.environment.browserDetails.viewportWidth` | `642` |
| SDK名稱 | SDK識別碼。 此欄位會使用URI來改善不同軟體程式庫所提供的識別碼之間的唯一性。 使用獨立程式庫時，值為 `https://ns.adobe.com/experience/alloy`. 當資料庫作為標籤擴充功能的一部分使用時，值為 `https://ns.adobe.com/experience/alloy+reactor`. | | `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |
| SDK版本 | 使用獨立程式庫時，值為程式庫版本。 將程式庫用作標籤擴充功能的一部分時，值是程式庫版本與標籤擴充功能版本的串連。 | | `events[].xdm.implementationDetails.version` | `2.1.0+2.1.3` |
| 環境 | 收集資料的環境。 Adobe Experience Platform Web SDK一律會將此欄位設為 `browser`. | | `events[].xdm.implementationDetails.environment` | `browser` |
| 當地時間 | 簡化延伸ISO格式的一般使用者本機時間戳記 [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `placeContext` | `events[].xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| 當地時區位移 | 使用者與GMT時差的分鐘數。 | `placeContext` | `events[].xdm.placeContext.localTimezoneOffset` | `360` |
| 時間戳記 | 簡化延伸ISO格式的一般使用者UTC時間戳記 [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | 一律包含 | `events[].xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |
| 目前頁面URL | 目前頁面的URL。 | `web` | `events[].xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| 反向連結URL | 造訪的上一個頁面的URL。 | `web` | `events[].xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}
