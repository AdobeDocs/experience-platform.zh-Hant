---
title: 在Adobe Experience PlatformWeb SDK中自動收集資訊
description: Adobe Experience PlatformSDK自動收集的每條資訊的概述。
keywords: 收集資訊；上下文；配置；設備；螢幕高度；螢幕高度；螢幕方向；螢幕寬度；螢幕寬度；環境；視口高度；視口高度；視口高度；視口寬度；視圖寬度；crowser詳細資訊；瀏覽器詳細資訊；實施詳細資訊；實現詳細資訊；名稱；版本；laceContext;localTime；本地時間zoneOffset；本地時區偏移；timestamp;web;url;webPageDetails;web頁詳細資訊；webReferer;web引用者；橫向；縱向；
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# 自動收集的資訊

Adobe Experience PlatformWeb SDK可自動收集大量資訊，而無需任何特殊配置。 但是，如果需要，可以使用 `context` 的上界 `configure` 的子菜單。 [請參閱配置SDK](../fundamentals/configuring-the-sdk.md)。 以下是這些資訊的清單。 括弧中的名稱表示配置上下文時要使用的字串。

## 裝置 (`device`)

有關設備的資訊。 這不包括可從用戶代理字串查找的伺服器端資料。

### 螢幕高度

| **負載中的路徑：** | **範例：** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

螢幕的高度（以像素為單位）。

### 螢幕方向

| **負載中的路徑：** | **可能的值:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` 或 `portrait` |

螢幕的方向。

### 螢幕寬度

| **負載中的路徑：** | **範例：** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

螢幕寬度（以像素為單位）。

## 環境 (`environment`)

有關瀏覽器環境的詳細資訊。

### 環境類型

瀏覽器

| **負載中的路徑：** | **範例：** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

體驗所通過的環境類型。 Adobe Experience PlatformWeb SDK始終將此設定為 `browser`。

### 視區高度

| **負載中的路徑：** | **範例：** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

瀏覽器的內容區域的高度（以像素為單位）。

### 視區寬度

| **負載中的路徑：** | **範例：** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

瀏覽器的內容區域寬度（像素）。

## 實施詳細資訊

有關用於收集事件的SDK的資訊。

### 名稱

| **負載中的路徑：** | **範例：** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

軟體開發工具包(SDK)標識符。  此欄位使用URI來改進由不同軟體庫提供的標識符之間的唯一性。 使用獨立庫時，值為 `https://ns.adobe.com/experience/alloy`。 當庫用作標籤擴展的一部分時，值為 `https://ns.adobe.com/experience/alloy+reactor`。

### 版本

| **負載中的路徑：** | **範例：** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

當使用獨立庫時，該值只是庫版本。 當庫用作標籤擴展的一部分時，這是庫版本和與「+」聯接的標籤擴展版本。 例如，如果庫版本為2.1.0，而標籤擴展版本為2.1.3，則值為 `2.1.0+2.1.3`。

### 環境

| **負載中的路徑：** | **範例：** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

收集資料的環境。 這始終設定為 `browser`。

## 放置上下文(`placeContext`)

有關最終用戶位置的資訊。

### 本地時間

| **負載中的路徑：** | **範例：** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

簡化的擴展ISO格式的最終用戶的本地時間戳 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6)。

### 本地時區偏移

| **負載中的路徑：** | **範例：** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

用戶從GMT偏移的分鐘數。

## 時間戳記

| **負載中的路徑：** | **範例：** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

事件的時間戳。  無法刪除上下文的此部分。

簡化的擴展ISO格式的最終用戶的UTC時間戳 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6)。

## Web詳細資訊(`web`)

有關用戶所在頁面的詳細資訊。

### 當前頁URL

| **負載中的路徑：** | **範例：** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

當前頁的URL。

### 引用者URL

| **負載中的路徑：** | **範例：** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

訪問的上一頁的URL。
