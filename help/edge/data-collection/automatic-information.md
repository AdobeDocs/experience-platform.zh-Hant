---
title: Adobe Experience Platform網頁SDK中自動收集的資訊
description: 概述Adobe Experience PlatformSDK自動收集的每項資訊。
keywords: 收集資訊；context;configure;device;screenHeight;screenOrientation;screenWidth;screenWidth;creenWidth;environment;viewport Height;viewport Width;crowserDetails；瀏覽器詳細資訊；implementationDetails;implement Details;imement Details;name;placeContext;localTime;localLation;localTime;localTimezoneOffset；本地時區偏移；timestamp;web;url;webPageDetails;webPage Details;webReferrer;web Referrer;landscape;portrait;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 0f671a967a67761e0cfef6fa0d022e3c3790c2d8
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 6%

---

# 自動收集的資訊

Adobe Experience Platform網頁SDK可自動收集許多資訊，毋需特殊設定。 不過，如果需要，可使用`configure`命令中的`context`選項禁用此資訊。 [請參閱設定SDK](../fundamentals/configuring-the-sdk.md)。以下是這些資訊的清單。 括弧中的名稱表示配置上下文時要使用的字串。

## 裝置 (`device`)

裝置相關資訊。 這不包括可從使用者代理字串在伺服器端查閱的資料。

### 螢幕高度

| **裝載中的路徑：** | **範例：** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

螢幕高度（以像素為單位）。

### 螢幕方向

| **裝載中的路徑：** | **可能的值:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` 或 `portrait` |

畫面的方向。

### 螢幕寬度

| **裝載中的路徑：** | **範例：** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

螢幕寬度（以像素為單位）。

## 環境 (`environment`)

瀏覽器環境的詳細資訊。

### 環境類型

瀏覽器

| **裝載中的路徑：** | **範例：** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

體驗所透過的環境類型。 Adobe Experience Platform網頁SDK一律將此設定為`browser`。

### 視區高度

| **裝載中的路徑：** | **範例：** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

瀏覽器內容區域的高度（以像素為單位）。

### 視區寬度

| **裝載中的路徑：** | **範例：** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

瀏覽器內容區域的寬度（以像素為單位）。

## 實作詳細資訊

用於收集事件的SDK相關資訊。

### 名稱

| **裝載中的路徑：** | **範例：** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

軟體開發套件(SDK)識別碼。  此欄位使用URI來改善不同軟體程式庫所提供之識別碼之間的唯一性。 使用獨立程式庫時，值為`https://ns.adobe.com/experience/alloy`。 當庫用作Platform launch擴展的一部分時，該值為`https://ns.adobe.com/experience/alloy+reactor`。

### 版本

| **裝載中的路徑：** | **範例：** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

當使用獨立程式庫時，其值只是程式庫版本。 當程式庫用作Platform launch副檔名時，這是程式庫版本和Platform launch副檔名版本，並加上&quot;+&quot;。 例如，如果程式庫版本為2.1.0，而Platform launch擴充功能版本為2.1.3，則值應為`2.1.0+2.1.3`。

### 環境

| **裝載中的路徑：** | **範例：** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

收集資料的環境。 這一律設為`browser`。

## 置入內容(`placeContext`)

有關最終用戶位置的資訊。

### 當地時間

| **裝載中的路徑：** | **範例：** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

簡化的擴充ISO格式[ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6)的使用者本機時間戳記。

### 局部時區偏移

| **裝載中的路徑：** | **範例：** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

用戶從GMT偏移的分鐘數。

## 時間戳記

| **裝載中的路徑：** | **範例：** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

事件的時間戳記。  無法移除此部分的內容。

簡化的擴展ISO格式[ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6)的最終用戶的UTC時間戳記。

## Web詳細資訊(`web`)

使用者所在頁面的詳細資訊。

### 目前頁面URL

| **裝載中的路徑：** | **範例：** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

目前頁面的URL。

### 反向連結URL

| **裝載中的路徑：** | **範例：** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

已造訪之上一頁的URL。
