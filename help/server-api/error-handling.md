---
title: 錯誤處理
description: 了解對Adobe Experience Platform Edge Network Server API執行API請求時可能遇到的錯誤。
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 3%

---

# 錯誤處理

## 總覽 {#overview}

Adobe Experience Platform Edge Network Server API中的API錯誤可能有多種原因，包括內部（邊緣網路本身）或外部（輸入、設定或上游相關）。

## 錯誤類型 {#error-types}

| 錯誤 | 類型 | 說明 | 狀態代碼 |
| --- | --- | --- | --- |
| `RequestProcessingError` | 內部 | Adobe Experience Platform邊緣網路針對非預期情況發出的一般用途錯誤。 | `500` |
| `InputError` | 外部 | 包括由錯誤的輸入導致的錯誤，以及實體驗證錯誤。 | `4xx` |
| `ConfigurationError` | 外部 | 伺服器端設定錯誤。 | `422` |
| `UpstreamError` | 外部 | 上游服務的通訊錯誤。 | `207 Multi-Status` |

## 嚴重性

伺服器API錯誤也可依嚴重性來分割：

* **致命錯誤** 將停止派送管道。
* **非致命錯誤** 可能會發出部分處理的訊號，同時允許請求處理繼續。
   * 如果存在，請求的整體狀態代碼將變更為 `207 Multi-Status`.

| 錯誤 | 類型 | 註釋 |
| --- | --- | --- |
| `RequestProcessingError` | 致命 | 在請求處理期間隨時可能發生。 |
| `InputError` | 致命 | 在上游發送請求前接受請求時發生。 |
| `ConfigurationError` | 致命 | 在上游發送請求前接受請求時發生。 |
| `UpstreamError` | 非致命 | 上游服務的通訊錯誤。 |

### 致命錯誤 {#fatal-errors}

嚴重錯誤會暫停請求處理，並導致傳回非2xx回應狀態。 查看 [錯誤類型](#error-types) 區段來查看與每個錯誤類型對應的預期狀態代碼。

錯誤會伴隨包含錯誤物件的回應本體。 在這種情況下，回應內文會包含問題詳細資料，如 [RFC 7807 HTTP API的問題詳細資訊](https://tools.ietf.org/html/rfc7807).

傳回的內容類型為 `application/problem+json` 媒體類型。 如果存在，此響應將包含與錯誤相關的機器可讀詳細資訊。 問題詳細資訊包括URI類型。

所有錯誤對象都有 `type`, `status`, `title`, `detail` 和 `report` 訊息屬性，讓API用戶端可以判斷問題所在。

| 屬性 | 類型 | 說明 |
| -------- | ------ | ----------- |
| `type` | 字串 | URI引用(RFC3986)，按照格式標識問題類型 `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | 數字 | 伺服器為此問題發生時生成的HTTP狀態代碼。 |
| `title` | 字串 | 問題類型的簡短、人類看得懂的摘要。 |
| `detail` | 字串 | 問題類型的簡短、人類看得懂的說明。 |
| `report` | 物件 | 協助偵錯的其他屬性的地圖，例如請求ID或組織ID。 在某些情況下，它可能包含現有錯誤的特定資料，例如驗證錯誤的清單。 |

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

### 非致命錯誤 {#non-fatal-errors}

非致命錯誤可進一步細分為：

* 錯誤：處理請求時發生但並未導致整個請求遭拒的問題(例如 非關鍵上游故障)。
* 警告：來自上游服務的消息，該消息可能指示已發生請求的部分處理。

遇到非致命錯誤時（不包括警告）, [!DNL Server API] 會將回應狀態變更為 `207 Multi-Status`.

另一方面，警告大多是提供資訊的，因為它們通常代表一種可能的暫時情況，而不會完全影響請求。 以下範例是在分段引擎中讀取的部分設定檔，在此情況下，準確度會受到某種程度的影響，但功能仍會提供。

非致命錯誤在 _問題詳細資訊_ 格式，但直接嵌入Edge網關的標準響應，該響應屬於 `application/json`.

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

## 處理 `4xx` 和 `5xx` 回應


| 錯誤代碼 | 說明 |
|---|---|
| `4xx Bad Request` | 最多 `4xx` 錯誤（如400、403、404）不應代表客戶重試，除非 `429`. 這些是客戶端錯誤，將無法成功。 用戶端必須先解決錯誤，才能重試請求。 |
| `429 Too Many Requests` | `429` HTTP回應代碼表示Adobe Experience Platform邊緣網路或上游服務正在速率限制要求。 在這種情況下，呼叫方必須遵守 `Retry-After` 回應標題。 任何回應都必須包含HTTP回應程式碼，且包含網域特定錯誤碼。 |
| `500 Internal Server Error` | `500` 錯誤是一般的、捕捉到全部的錯誤。 `500` 不得重試錯誤，但 `502` 和 `503`. 中介機構必須以 `500` 錯誤，可能會以一般錯誤碼/訊息或更特定於網域的錯誤碼/訊息回應。 |
| `502 Bad Gateway` | 指出Adobe Experience Platform邊緣網路收到來自上游伺服器的無效回應。 這可能會因為伺服器之間的網路問題而發生。 臨時網路問題可能已解決，因此重試可能會解決問題，因此，的收件者 `502` 錯誤可能會在一段時間後重試請求。 |
| `503 Service Unavailable` | 此錯誤代碼表示服務暫時不可用。 在維護期間可能會發生此情況。 收件者 `503` 錯誤可能會重試請求，但必須符合 `Retry-After` 頁首。 |
| `504 Gateway Timeout` | 指出向上游伺服器發出的Adobe Experience Platform邊緣網路請求已逾時。 這可能會因為伺服器之間的網路問題、 DNS問題或其他網路問題而發生。 暫時的網路問題可以在一段時間後解決，而重試可能會解決問題。 |
