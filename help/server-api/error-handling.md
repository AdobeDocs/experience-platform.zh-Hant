---
title: 錯誤處理
description: 瞭解在對Adobe Experience Platform邊緣網路伺服器API執行API請求時可能遇到的錯誤。
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 3%

---

# 錯誤處理

## 總覽 {#overview}

Adobe Experience Platform邊緣網路伺服器API中的API錯誤可能有多種原因，包括內部（邊緣網路本身）或外部（輸入、配置或上游相關）。

## 錯誤類型 {#error-types}

| 錯誤 | 類型 | 說明 | 狀態代碼 |
| --- | --- | --- | --- |
| `RequestProcessingError` | 內部 | Adobe Experience Platform邊緣網路在意外情況下發出的通用錯誤。 | `500` |
| `InputError` | 外部 | 包括錯誤輸入導致的錯誤以及實體驗證錯誤。 | `4xx` |
| `ConfigurationError` | 外部 | 伺服器端配置錯誤。 | `422` |
| `UpstreamError` | 外部 | 上游服務的通信錯誤。 | `207 Multi-Status` |

## 嚴重性

伺服器API錯誤也可按嚴重性分解：

* **錯誤** 會阻止派送管道。
* **非致命錯誤** 可能發出部分處理信號，同時允許請求處理繼續。
   * 當存在時，請求的整體狀態代碼將更改為 `207 Multi-Status`。

| 錯誤 | 類型 | 註釋 |
| --- | --- | --- |
| `RequestProcessingError` | 致命 | 在請求處理過程中的任何時刻都可能發生。 |
| `InputError` | 致命 | 在上游調度請求之前，在接受請求時發生。 |
| `ConfigurationError` | 致命 | 在上游調度請求之前，在接受請求時發生。 |
| `UpstreamError` | 非致命 | 上游服務的通信錯誤。 |

### 錯誤 {#fatal-errors}

嚴重錯誤會停止請求處理並導致返回非2xx響應狀態。 查看 [錯誤類型](#error-types) 部分，查看與每個錯誤類型對應的預期狀態代碼。

錯誤將伴隨包含錯誤對象的響應主體。 在這種情況下，響應主體包含問題詳細資訊，定義如下 [RFC 7807 HTTP API問題詳細資訊](https://tools.ietf.org/html/rfc7807)。

返回的內容類型是 `application/problem+json` 媒體類型。 當存在時，此響應包含與錯誤相關的機器可讀詳細資訊。 問題詳細資訊包括URI類型。

所有錯誤對象 `type`。 `status`。 `title`。 `detail` 和 `report` 消息屬性，以便API客戶端能夠判斷問題所在。

| 屬性 | 類型 | 說明 |
| -------- | ------ | ----------- |
| `type` | 字串 | URI引用(RFC3986)，它按照格式標識問題類型 `https://ns.adobe.com/aep/errors/<ERROR-CODE>`。 |
| `status` | 數字 | 伺服器為此問題生成的HTTP狀態代碼。 |
| `title` | 字串 | 問題類型的簡短的、可人讀的摘要。 |
| `detail` | 字串 | 問題類型的簡短、人可讀的描述。 |
| `report` | 物件 | 幫助調試的其他屬性（如請求ID或組織ID）的映射。 在某些情況下，它可能包含特定於現有錯誤的資料，如驗證錯誤清單。 |

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

* 錯誤：處理請求時發生但未導致整個請求被拒絕的問題(例如 非臨界上游故障)。
* 警告：來自上游服務的消息，該消息可能指示已對請求進行部分處理。

遇到非致命錯誤（不包括警告）時， [!DNL Server API] 將響應狀態更改為 `207 Multi-Status`。

另一方面，警告大多是資訊性的，因為它們通常代表一種可能暫時的情況，而這種情況並未對請求產生完全影響。 這裡的一個示例是在分段引擎中讀取的部分輪廓，在這種情況下，精度會受到一定程度的影響，但功能仍然被提供。

非致命錯誤在 _問題詳細資訊_ 格式，但是直接嵌入到Edge網關的標準響應中， `application/json`。

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

## 處理 `4xx` 和 `5xx` 響應


| 錯誤代碼 | 說明 |
|---|---|
| `4xx Bad Request` | 最多 `4xx` 不應代表客戶端重試錯誤（如400、403、404），除非 `429`。 這些是客戶端錯誤，不會成功。 客戶端必須先解決錯誤，然後才能重試請求。 |
| `429 Too Many Requests` | `429` HTTP響應代碼表示Adobe Experience Platform邊緣網路或上游服務是速率限制請求。 在這種情況下，調用方必須尊重 `Retry-After` 響應標頭。 返回的任何響應都必須攜帶具有域特定錯誤代碼的HTTP響應代碼。 |
| `500 Internal Server Error` | `500` 錯誤是一般錯誤，捕獲所有錯誤。 `500` 不能重試錯誤， `502` 和 `503`。 中間商必須用 `500` 錯誤，並可能使用一般錯誤代碼/消息或更多域特定的錯誤代碼/消息進行響應。 |
| `502 Bad Gateway` | 指示Adobe Experience Platform邊緣網路從上游伺服器收到無效響應。 這可能是由於伺服器之間的網路問題造成的。 臨時網路問題可以解決，因此重試可以解決該問題，因此收件人 `502` 錯誤可能會在一段時間後重試請求。 |
| `503 Service Unavailable` | 此錯誤代碼表示服務暫時不可用。 在維護期間可能會發生這種情況。 收件人 `503` 錯誤可能會重試請求，但必須尊重 `Retry-After` 標題。 |
| `504 Gateway Timeout` | 指示對上游伺服器的Adobe Experience Platform邊緣網路請求已超時。 這可能是由於伺服器之間的網路問題、DNS問題或其他網路問題。 臨時網路問題可以在一段時間後解決，重試可以解決該問題。 |
