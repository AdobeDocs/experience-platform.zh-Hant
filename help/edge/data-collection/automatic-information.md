---
title: 在Adobe Experience Platform Web SDK中自動收集的資訊
description: Adobe Experience Platform SDK自動收集的每一項資訊概覽。
keywords: 收集資訊；內容；設定；裝置；screenHeight；熒幕高度；熒幕方向；熒幕方向；熒幕寬度；環境；檢視區高度；檢視區高度；檢視區寬度；檢視區寬度；crowserDetails；瀏覽器詳細資料；implementationDetails；實作詳細資料；名稱；版本；placeContext；localTime；localTime；localTimezoneOffset；本機時區位移；時間戳記；網頁；url；webPageDetails；網頁詳細資料；webReferrer；網頁反向連結；橫向；直向；
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: e3f507e010ea2a32042b53d46795d87e82e3fb72
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# 自動收集的資訊

Adobe Experience Platform Web SDK會自動收集許多資訊片段，不需要任何特殊設定。 不過，如有需要，可透過以下方式停用此資訊： `context` 中的選項 `configure` 命令。 [請參閱設定SDK](../fundamentals/configuring-the-sdk.md). 以下是這些資訊的清單。 括弧內的名稱表示設定內容時要使用的字串。

## 裝置 (`device`)

裝置的相關資訊。 這不包括可從使用者代理字串在伺服器端查閱的資料。

### 熒幕高度

| **承載中的路徑：** | **範例：** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

熒幕的高度（畫素）。

### 熒幕方向

| **承載中的路徑：** | **可能的值:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` 或 `portrait` |

熒幕方向。

### 熒幕寬度

| **承載中的路徑：** | **範例：** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

熒幕的寬度（畫素）。

## 環境 (`environment`)

有關瀏覽器環境的詳細資訊。

### 環境類型

瀏覽器

| **承載中的路徑：** | **範例：** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

體驗出現的環境型別。 Adobe Experience Platform Web SDK一律會將此專案設為 `browser`.

### 檢視區高度

| **承載中的路徑：** | **範例：** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

瀏覽器內容區域的高度（畫素）。

### 檢視區寬度

| **承載中的路徑：** | **範例：** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

瀏覽器內容區域的寬度（畫素）。

## 實作詳細資料

有關用於收集事件的SDK的資訊。

### 名稱

| **承載中的路徑：** | **範例：** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

軟體開發套件(SDK)識別碼。  此欄位會使用URI來改善不同軟體程式庫所提供的識別碼之間的唯一性。 使用獨立程式庫時，值為 `https://ns.adobe.com/experience/alloy`. 當資料庫作為標籤擴充功能的一部分使用時，值為 `https://ns.adobe.com/experience/alloy+reactor`.

### 版本

| **承載中的路徑：** | **範例：** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

使用獨立程式庫時，值只是程式庫版本。 將程式庫當作標籤擴充功能的一部分使用時，此即為程式庫版本和使用「+」連線的標籤擴充功能版本。 例如，如果程式庫版本是2.1.0，而標籤擴充功能版本是2.1.3，則值將是 `2.1.0+2.1.3`.

### 環境 {#environment}

| **承載中的路徑：** | **範例：** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

收集資料的環境。 此一律設為 `browser`.

## 地標內容(`placeContext`) {#place-context}

有關一般使用者位置的資訊。

### 當地時間

| **承載中的路徑：** | **範例：** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

簡化延伸ISO格式的一般使用者本機時間戳記 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### 當地時區位移

| **承載中的路徑：** | **範例：** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

使用者與GMT時差的分鐘數。

## 時間戳記

| **承載中的路徑：** | **範例：** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

事件的時間戳記。  無法移除這個部分的內容。

簡化延伸ISO格式的一般使用者UTC時間戳記 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## 網頁詳細資料(`web`)

有關使用者所在頁面的詳細資料。

### 目前頁面URL

| **承載中的路徑：** | **範例：** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

目前頁面的URL。

### 反向連結URL

| **承載中的路徑：** | **範例：** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

造訪的上一個頁面的URL。
