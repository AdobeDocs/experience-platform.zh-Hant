---
keywords: Experience Platform；首頁；熱門主題；串流；串流內嵌；串流內嵌驗證；驗證；串流內嵌驗證；驗證；同步驗證；同步驗證；非同步驗證；非同步驗證；非同步驗證；
solution: Experience Platform
title: 串流擷取驗證
type: Tutorial
description: 串流內嵌可讓您使用串流端點即時將資料上傳至Adobe Experience Platform。 串流獲取API支援同步和非同步兩種驗證模式。
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 3%

---

# 串流內嵌驗證

串流內嵌可讓您使用串流端點即時將資料上傳至Adobe Experience Platform。 串流獲取API支援同步和非同步兩種驗證模式。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md):資料可傳送至的方法之一 [!DNL Experience Platform].

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括 [!DNL Schema Registry]，會與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- Content-Type: `application/json`

### 驗證涵蓋範圍

[!DNL Streaming Validation Service] 涵蓋下列方面的驗證：
- Range
- 是否存在
- 列舉
- 模式
- 類型
- 格式

## 同步驗證

同步驗證是一種驗證方法，可立即回饋擷取失敗的原因。 但是，失敗時，驗證失敗的記錄會遭到捨棄，且無法傳送至下游。 因此，同步驗證只應在開發程式期間使用。 執行同步驗證時，會通知呼叫者XDM驗證的結果，以及失敗的原因。

預設情況下，不會開啟同步驗證。 若要啟用，您必須傳入選用的查詢參數 `syncValidation=true` 進行API呼叫時。 此外，目前只有在資料流端點位於VA7資料中心時，才可使用同步驗證。

>[!NOTE]
>
>此 `syncValidation` 查詢參數僅適用於單條消息終結點，不能用於批處理終結點。

如果訊息在同步驗證期間失敗，訊息將不會寫入輸出佇列，而會立即為使用者提供意見反應。

>[!NOTE]
>
>架構變更可能不會立即可用，因為系統會快取變更。 快取最多需要15分鐘才能重新整理。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `id` 串流連線的值。 |

**要求**

提交下列請求，透過同步驗證將資料內嵌至您的資料入口：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 您要擷取之資料的JSON內文。 |

**回應**

啟用同步驗證後，成功的回應會在其裝載中包含任何遇到的驗證錯誤：

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

上述回應會列出發現多少個架構違規，以及有哪些違規。 例如，此回應會指出鍵值 `workEmail` 和 `person` 未在架構中定義，因此不允許。 也會標籤 `_id` 不正確，因為架構應為 `string`，但 `long` 已插入。 請注意，一旦遇到五個錯誤，驗證服務就會 **停止** 正在處理該訊息。 不過，其他訊息會繼續剖析。

## 非同步驗證

非同步驗證是驗證方法，不會立即提供反饋。 而是會將資料傳送至中失敗的批次 [!DNL Data Lake] 防止資料丟失。 稍後可以檢索此失敗資料，以便進一步分析和重播。 此方法應用於生產中。 除非另有要求，串流擷取會以非同步驗證模式運作。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `id` 串流連線的值。 |

**要求**

提交下列請求，透過非同步驗證將資料內嵌至您的資料入口：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 您要擷取之資料的JSON內文。 |

>[!NOTE]
>
>不需要額外的查詢參數，因為預設會啟用非同步驗證。

**回應**

啟用非同步驗證後，成功的回應會傳回下列內容：

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "syncValidation": {
        "skipped": true
    }
}
```

請注意，響應如何表示已跳過同步驗證，因為尚未明確請求同步驗證。

## 附錄

本節包含各種狀態代碼對於擷取資料之回應有何意義的相關資訊。

### 狀態代碼

| 狀態代碼 | 這意味著什麼 |
| ----------- | ------------- |
| 200 | 成功. 對於同步驗證，這表示已通過驗證檢查。 對於非同步驗證，這表示它只成功接收了訊息。 使用者可以透過觀察資料集來找出最終訊息狀態。 |
| 400 | 錯誤. 你的請求有問題。 從串流驗證服務收到含有詳細資訊的錯誤訊息。 |
| 401 | 錯誤. 您的要求未授權 — 您需要使用不記名代號來要求。 如需如何要求存取權的詳細資訊，請查看 [教學課程](https://www.adobe.com/go/platform-api-authentication-en) 或 [部落格貼文](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | 錯誤. 內部系統錯誤。 |
| 501 | 錯誤. 這表示同步驗證是 **not** 支援此位置。 |
| 503 | 錯誤. 服務當前不可用。 客戶端應使用指數式回退策略至少重試三次。 |
