---
title: 自動收集的資訊
seo-title: Adobe Experience Platform Web SDK自動收集的資訊
description: Adobe Experience Cloud SDK自動收集的每項資訊說明
seo-description: Adobe Experience Cloud SDK自動收集的每項資訊說明
keywords: collect information;context;configure;device;screenHeight;screen Height;screenOrientation;screen Orientation;screenWidth;screen Width;environment;viewportHeight;viewport Height;viewportWidth;viewport Width;crowserDetails;browser details;implementationDetails;implementation Details;name;version;placeContext;localTime;local Time;localTimezoneOffset;local Timezone Offset;timestamp;web;url;webPageDetails;web Page Details;webReferrer;web Referrer;landscape;portrait;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 8%

---


# 自動收集的資訊

Adobe Experience Cloud SDK會自動收集多項資訊，毋需任何特殊設定。 不過，如果需要，可使用命令中的選項 `context` 禁用此信 `configure` 息。 [請參閱設定SDK](../fundamentals/configuring-the-sdk.md)。 以下是這些資訊的清單。 括弧中的名稱表示配置上下文時要使用的字串。

## 裝置 (`device`)

裝置相關資訊。 這不包括可從使用者代理字串在伺服器端查閱的資料。

### 螢幕高度

| **裝載中的路徑：** | **範例：** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

螢幕的像素高度。

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

體驗所處環境的類型。 JavaScript專用的Adobe Experience Platform SDK一律會設定 `browser`。

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

軟體開發套件(SDK)識別碼。  此欄位使用URI來改善不同軟體程式庫所提供之識別碼之間的唯一性。

### 版本

| **裝載中的路徑：** | **範例：** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

### 環境

| **裝載中的路徑：** | **範例：** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |


## 置入內容(`placeContext`)

有關最終用戶位置的資訊。

### 當地時間

| **裝載中的路徑：** | **範例：** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

簡化的擴充ISO格式 [ISO 8601的使用者本機時間戳記](https://tools.ietf.org/html/rfc3339#section-5.6)。

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

UTC時間戳記，適用於簡化的ISO擴充格式 [ISO 8601的使用者](https://tools.ietf.org/html/rfc3339#section-5.6)。

## 網頁詳細資訊(`web`)

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
