---
title: 在Adobe Experience Platform Web SDK中自動收集資訊
description: Adobe Experience Platform SDK自動收集之每項資訊的概述。
keywords: 收集資訊；內容；設定；裝置；螢幕高度；螢幕方向；螢幕方向；螢幕寬度；環境；檢視區高度；檢視區寬度；crowserDetails；瀏覽器詳細資料；實作詳細資料；實作詳細資料；名稱；版本；placeContext;localTimezoneOffset；本地時區偏移；時間戳記；網頁；Web頁面詳細資料；橫向；Web反向連結；網頁詳細資料；橫向；
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# 自動收集的資訊

Adobe Experience Platform Web SDK可自動收集許多資訊，無需任何特殊設定。 不過，如有需要，可使用 `context` 選項 `configure` 命令。 [請參閱設定SDK](../fundamentals/configuring-the-sdk.md). 下面是這些資訊的清單。 括弧中的名稱表示設定上下文時要使用的字串。

## 裝置 (`device`)

有關設備的資訊。 這不包括可從使用者代理字串在伺服器端查詢的資料。

### 螢幕高度

| **裝載中的路徑：** | **範例：** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

螢幕的高度（像素）。

### 螢幕方向

| **裝載中的路徑：** | **可能的值:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` 或 `portrait` |

螢幕的方向。

### 螢幕寬度

| **裝載中的路徑：** | **範例：** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

螢幕的寬度（像素）。

## 環境 (`environment`)

瀏覽器環境的詳細資訊。

### 環境類型

瀏覽器

| **裝載中的路徑：** | **範例：** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

體驗隨之呈現的環境類型。 Adobe Experience Platform Web SDK一律將此值設為 `browser`.

### 檢視區高度

| **裝載中的路徑：** | **範例：** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

瀏覽器內容區域的高度（像素）。

### 檢視區寬度

| **裝載中的路徑：** | **範例：** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

瀏覽器內容區域的寬度（像素）。

## 實作詳細資料

用於收集事件之SDK的相關資訊。

### 名稱

| **裝載中的路徑：** | **範例：** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

軟體開發套件(SDK)識別碼。  此欄位使用URI來改進由不同軟體庫提供的標識符之間的唯一性。 使用獨立程式庫時，值為 `https://ns.adobe.com/experience/alloy`. 當程式庫用作標籤擴充功能的一部分時，值為 `https://ns.adobe.com/experience/alloy+reactor`.

### 版本

| **裝載中的路徑：** | **範例：** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

使用獨立程式庫時，值只是程式庫版本。 當程式庫用作標籤擴充功能的一部分時，此為程式庫版本，以及以「+」連結的標籤擴充功能版本。 例如，如果程式庫版本為2.1.0，而標籤擴充功能版本為2.1.3，則值會是 `2.1.0+2.1.3`.

### 環境

| **裝載中的路徑：** | **範例：** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

收集資料的環境。 此值一律設為 `browser`.

## 放置上下文(`placeContext`)

有關最終用戶位置的資訊。

### 當地時間

| **裝載中的路徑：** | **範例：** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

簡化的擴展ISO格式的最終用戶的本地時間戳 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### 本地時區偏移

| **裝載中的路徑：** | **範例：** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

使用者在GMT時間差的分鐘數。

## 時間戳記

| **裝載中的路徑：** | **範例：** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

事件的時間戳記。  無法移除這部分內容。

簡化的ISO擴展格式的最終用戶的UTC時間戳 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

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

造訪的上一頁的URL。
