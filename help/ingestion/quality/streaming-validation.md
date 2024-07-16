---
keywords: Experience Platform；首頁；熱門主題；串流；串流擷取；串流擷取驗證；驗證；串流擷取驗證；驗證；同步驗證；同步驗證；非同步驗證；非同步驗證；
solution: Experience Platform
title: 串流擷取驗證
type: Tutorial
description: 串流內嵌可讓您使用串流端點即時將資料上傳到Adobe Experience Platform。 串流獲取API支援兩種驗證模式 — 同步和非同步。
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 11%

---

# 串流擷取驗證

串流內嵌可讓您使用串流端點即時將資料上傳到Adobe Experience Platform。 串流獲取API支援兩種驗證模式 — 同步和非同步。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md)：資料可傳送至[!DNL Experience Platform]的其中一種方法。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Schema Registry]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

- Content-Type： `application/json`

### 驗證涵蓋範圍

[!DNL Streaming Validation Service]涵蓋下列領域的驗證：
- Range
- 是否存在
- 列舉
- 模式
- 類型
- 格式

## 同步驗證

同步驗證是一種驗證方法，可針對擷取失敗的原因提供立即回饋。 但是，失敗時，會捨棄驗證失敗的記錄，並防止其傳送到下游。 因此，同步驗證只應在開發程式中使用。 執行同步驗證時，會向呼叫者通知XDM驗證的結果，以及失敗的原因（如果失敗）。

依預設，同步驗證不會開啟。 若要啟用，您必須在進行API呼叫時傳入選用查詢引數`syncValidation=true`。 此外，目前只有在您的串流端點位於VA7資料中心時，才能使用同步驗證。

>[!NOTE]
>
>`syncValidation`查詢引數僅適用於單一訊息端點，且無法用於批次端點。

如果訊息在同步驗證期間失敗，則不會將訊息寫入輸出佇列，這會為使用者提供立即的回饋。

>[!NOTE]
>
>結構描述變更可能無法立即使用，因為會快取變更。 快取最多只需15分鐘重新整理。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前建立的串流連線的`id`值。 |

**要求**

提交下列請求，以透過同步驗證將資料擷取至您的資料入口：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 您要內嵌之資料的JSON內文。 |

**回應**

啟用同步驗證後，成功的回應會在其承載中包含任何遇到的驗證錯誤：

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

上述回應會列出找到多少綱要違規，以及違規內容。 例如，此回應指出結構描述中未定義索引鍵`workEmail`和`person`，因此不允許使用。 它也會將`_id`的值標示為不正確，因為結構描述預期為`string`，但插入的是`long`。 請注意，一旦發生5個錯誤，驗證服務將&#x200B;**停止**&#x200B;處理該訊息。 不過，其他訊息仍會繼續剖析。

## 非同步驗證

非同步驗證是一種不會立即提供回饋的驗證方法。 相反地，資料會傳送到[!DNL Data Lake]中失敗的批次，以防止資料遺失。 此失敗的資料稍後可擷取，以供進一步分析和重播。 此方法應用於生產環境。 除非另有要求，否則串流擷取會以非同步驗證模式運作。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前建立的串流連線的`id`值。 |

**要求**

提交下列請求，以透過非同步驗證將資料擷取至您的資料入口：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 您要內嵌之資料的JSON內文。 |

>[!NOTE]
>
>不需要額外的查詢引數，因為預設會啟用非同步驗證。

**回應**

啟用非同步驗證時，成功的回應會傳回以下內容：

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

請注意，回應指出已略過同步驗證，因為並未明確要求同步驗證。

## 附錄

本節包含各種狀態代碼對於擷取資料的回應有何意義的資訊。

### 狀態代碼

| 狀態代碼 | 其含義 |
| ----------- | ------------- |
| 200 | 成功。 對於同步驗證，這表示它已通過驗證檢查。 針對非同步驗證，這表示其僅已成功收到訊息。 使用者可透過觀察資料集來瞭解最終的訊息狀態。 |
| 400 | 錯誤。 您的請求發生問題。 從串流驗證服務收到包含進一步詳細資訊的錯誤訊息。 |
| 401 | 錯誤。 您的請求未獲授權 — 您需要以持有人權杖請求。 如需有關如何要求存取許可權的詳細資訊，請參閱此[教學課程](https://www.adobe.com/go/platform-api-authentication-en)或此[部落格](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)。 |
| 500 | 錯誤。 發生內部系統錯誤。 |
| 501 | 錯誤。 這表示此位置&#x200B;**不支援**&#x200B;同步驗證。 |
| 503 | 錯誤。 服務目前無法使用。 使用者端應使用指數回退策略至少重試三次。 |
