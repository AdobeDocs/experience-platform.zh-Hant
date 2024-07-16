---
title: 錯誤處理
description: 瞭解當您對Adobe Experience PlatformEdge Network伺服器API執行API請求時可能遇到的錯誤。
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 2%

---

# 錯誤處理

## 概觀 {#overview}

Adobe Experience PlatformEdge Network伺服器API中的API錯誤有多種原因，包括內部(Edge Network本身)或外部（輸入、設定或上游相關）。

## 錯誤型別 {#error-types}

| 錯誤 | 類型 | 說明 | 狀態代碼 |
| --- | --- | --- | --- |
| `RequestProcessingError` | 內部 | Adobe Experience PlatformEdge Network在意外情況下發出的一般用途錯誤。 | `500` |
| `InputError` | 外部 | 包含由錯誤輸入造成的錯誤以及實體驗證錯誤。 | `4xx` |
| `ConfigurationError` | 外部 | 伺服器端設定錯誤。 | `422` |
| `UpstreamError` | 外部 | 與上游服務的通訊錯誤。 | `207 Multi-Status` |

## 嚴重性

伺服器API錯誤也可以依嚴重程度分割：

* **嚴重錯誤**&#x200B;將停止分派管道。
* **非嚴重錯誤**&#x200B;可能表示有部分處理，但允許繼續處理要求。
   * 當出現時，請求的整體狀態代碼將變更為`207 Multi-Status`。

| 錯誤 | 類型 | 備註 |
| --- | --- | --- |
| `RequestProcessingError` | 致命 | 處理要求期間的任何時間點都可能發生。 |
| `InputError` | 致命 | 接受請求時，在將其分派到上游之前發生。 |
| `ConfigurationError` | 致命 | 接受請求時，在將其分派到上游之前發生。 |
| `UpstreamError` | 非致命 | 與上游服務的通訊錯誤。 |

### 嚴重錯誤 {#fatal-errors}

嚴重錯誤會停止要求處理，並造成傳回非2xx回應狀態。 請檢視[錯誤型別](#error-types)區段以檢視每個錯誤型別對應的預期狀態代碼。

錯誤會隨附包含錯誤物件的回應內文。 在此情況下，回應本文包含由[RFC 7807 HTTP API的問題詳細資料](https://tools.ietf.org/html/rfc7807)所定義的問題詳細資料。

傳回的內容型別是`application/problem+json`媒體型別。 當出現時，此回應會包含與錯誤相關的機器可讀詳細資訊。 問題詳細資料包括URI型別。

所有錯誤物件都有`type`、`status`、`title`、`detail`和`report`訊息屬性，以便API使用者端能夠指出問題所在。

| 屬性 | 類型 | 說明 |
| -------- | ------ | ----------- |
| `type` | 字串 | 識別問題型別的URI參照(RFC3986)，格式為`https://ns.adobe.com/aep/errors/<ERROR-CODE>`。 |
| `status` | 數字 | 伺服器針對此問題發生所產生的HTTP狀態碼。 |
| `title` | 字串 | 簡短、易讀的問題型別摘要。 |
| `detail` | 字串 | 問題型別的簡短說明（人類看得懂的描述）。 |
| `report` | 物件 | 協助進行偵錯的其他屬性地圖，例如請求ID或組織ID。 在某些情況下，它可能包含手頭錯誤的特定資料，例如驗證錯誤清單。 |

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0104-422",
   "status":422,
   "title":"Unprocessable entity",
   "detail":"Invalid request (report attached). Please check your input and try again.",
   "report":{
      "errors":[
         "Allowed Adobe version is 1.0 for standard 'Adobe' at index 0",
         "Allowed IAB version is 2.0 for standard 'IAB TCF' at index 1",
         "IAB consent string value must not be empty for standard 'IAB TCF' at index 1"
      ],
      "requestId":"0f8821e5-ed1a-4301-b445-5f336fb50ee8",
      "orgId":"53A16ACB5CC1D3760A495C99@AdobeOrg"
   }
}
```

### 非嚴重錯誤 {#non-fatal-errors}

非嚴重錯誤可進一步細分為：

* 錯誤：處理請求時發生錯誤，但未導致整個請求被拒絕的問題(例如 非關鍵上游失敗)。
* 警告：來自上游服務的訊息，可能表示發生了請求的部分處理。

發生非嚴重錯誤（排除警告）時，[!DNL Server API]會將回應狀態變更為`207 Multi-Status`。

另一方面，警告大多提供資訊，因為它們通常代表潛在的暫時性狀況，不會完全影響請求。 以下範例是區段引擎中讀取的部分設定檔，在此情況下，準確度會在一定程度上受到影響，但功能仍會提供。

非嚴重錯誤以&#x200B;_問題詳細資料_&#x200B;格式表示，但直接內嵌於Edge閘道的`application/json`型別標準回應。

```json
{
  "requestId": "72eaa048-207e-4dde-bf16-0cb2b21336d5",
  "handle": [
  ],
  "errors": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0201-503",
      "status": 503,
      "title": "The 'com.adobe.experience.platform.ode' service is temporarily unable to serve this request. Please try again later."
    }
  ],
  "warnings": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0204-200",
      "status": 200,
      "title": "A warning occurred while calling the 'com.adobe.audiencemanager' service for this request.",
      "report": {
        "cause": {
          "message": "Cannot read related customer for device id: ...",
          "code": 202
        }
      }
    }
  ]
}
```

## 正在處理`4xx`和`5xx`個回應

| 錯誤代碼 | 說明 |
|---|---|
| `4xx Bad Request` | 除了`429`以外，大部分的`4xx`錯誤（例如400、403、404）不應代表使用者端重試。 這些是使用者端錯誤，將不會成功。 使用者端必須先解決錯誤，才能重試要求。 |
| `429 Too Many Requests` | `429` HTTP回應代碼指出Adobe Experience PlatformEdge Network或上游服務正在限制要求的速率。 在此情況下，在此情況下，呼叫者必須遵守`Retry-After`回應標頭。 任何回流的回應都必須攜帶HTTP回應代碼以及網域特定的錯誤代碼。 |
| `500 Internal Server Error` | `500`個錯誤是一般、全包錯誤。 `500`錯誤不可重試，`502`和`503`除外。 中介必須以`500`錯誤回應，而且可能會以一般錯誤碼/訊息回應，或是以網域特定的錯誤碼/訊息回應。 |
| `502 Bad Gateway` | 指出Adobe Experience PlatformEdge Network從上游伺服器收到無效的回應。 這可能是因為伺服器之間的網路問題所造成。 暫時的網路問題可能解決，因此重試可能會解決問題，因此`502`錯誤的收件者可能會在一段時間後重試要求。 |
| `503 Service Unavailable` | 此錯誤碼表示服務暫時無法使用。 這可能發生在維護期間。 `503`錯誤的收件者可能會重試該要求，但必須遵守`Retry-After`標頭。 |
| `504 Gateway Timeout` | 指出對上游伺服器的Adobe Experience PlatformEdge Network要求已逾時。 這可能是因為伺服器之間的網路問題、DNS問題或其他網路問題所造成。 一段時間後，暫時性的網路問題可能會得到解決，重試可能會解決問題。 |
