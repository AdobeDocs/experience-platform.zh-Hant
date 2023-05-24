---
keywords: Experience Platform；首頁；熱門主題；流；流；流；流；流；接收；驗證；流；接收；驗證；同步驗證；同步驗證；非同步驗證；非同步驗證；
solution: Experience Platform
title: 流式接收驗證
type: Tutorial
description: 流式處理接收允許您使用流式處理端點將資料即時上傳到Adobe Experience Platform。 流式接收API支援同步和非同步兩種驗證模式。
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 3%

---

# 流式接收驗證

流式處理接收允許您使用流式處理端點將資料即時上傳到Adobe Experience Platform。 流式接收API支援同步和非同步兩種驗證模式。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md):資料可通過其發送到的方法之一 [!DNL Experience Platform]。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Schema Registry]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

- Content-Type: `application/json`

### 驗證範圍

[!DNL Streaming Validation Service] 包括以下方面的驗證：
- Range
- 存在
- 枚舉
- 模式
- 類型
- 格式

## 同步驗證

同步驗證是一種驗證方法，可立即反饋接收失敗的原因。 但是，在失敗時，驗證失敗的記錄將被丟棄，並且無法向下游發送。 因此，同步驗證只應在開發過程中使用。 執行同步驗證時，將通知呼叫方XDM驗證的結果，如果失敗，則告知失敗原因。

預設情況下，不啟用同步驗證。 要啟用它，必須傳遞可選查詢參數 `syncValidation=true` 進行API調用時。 此外，當前只有流端點位於VA7資料中心時，同步驗證才可用。

>[!NOTE]
>
>的 `syncValidation` query參數僅可用於單個消息終結點，不能用於批處理終結點。

如果消息在同步驗證期間失敗，則消息不會寫入輸出隊列，這會為用戶提供即時反饋。

>[!NOTE]
>
>由於快取了更改，架構更改可能不會立即可用。 允許最多15分鐘快取刷新。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `id` 先前建立的流連接的值。 |

**要求**

提交以下請求，通過同步驗證將資料接收到資料輸入：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 要攝取的資料的JSON正文。 |

**回應**

啟用同步驗證後，成功的響應在其負載中包括遇到的任何驗證錯誤：

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

上述響應列出了發現多少架構違規，以及哪些違規。 例如，此響應表示 `workEmail` 和 `person` 未在架構中定義，因此不允許。 它還標籤 `_id` 不正確，因為架構應為 `string`，但 `long` 已插入。 請注意，一旦遇到五個錯誤，驗證服務將 **停止** 正在處理該消息。 但是，其他消息將繼續被分析。

## 非同步驗證

非同步驗證是一種驗證方法，不提供即時反饋。 相反，資料將發送到中的失敗批 [!DNL Data Lake] 防止資料丟失。 稍後可以檢索此失敗資料以進行進一步分析和重放。 該方法應用於生產中。 除非另有請求，否則流接收在非同步驗證模式下運行。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `id` 先前建立的流連接的值。 |

**要求**

提交以下請求，通過非同步驗證將資料接收到資料輸入：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 要攝取的資料的JSON正文。 |

>[!NOTE]
>
>不需要額外的查詢參數，因為預設情況下啟用了非同步驗證。

**回應**

啟用非同步驗證後，成功的響應將返回以下內容：

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

請注意響應如何表示已跳過同步驗證，因為尚未明確請求同步驗證。

## 附錄

本節包含有關各種狀態代碼對於接收資料的響應意味著什麼的資訊。

### 狀態代碼

| 狀態代碼 | 這意味著什麼 |
| ----------- | ------------- |
| 200 | 成功. 對於同步驗證，這意味著它已通過驗證檢查。 對於非同步驗證，這意味著它僅成功接收了消息。 用戶可以通過觀察資料集瞭解最終的消息狀態。 |
| 400 | 錯誤. 你的請求有問題。 從流驗證服務接收包含詳細資訊的錯誤消息。 |
| 401 | 錯誤. 您的請求未經授權 — 您需要使用持有者令牌進行請求。 有關如何請求訪問的詳細資訊，請查看此 [教程](https://www.adobe.com/go/platform-api-authentication-en) 或 [部落格帖子](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)。 |
| 500 | 錯誤. 內部系統錯誤。 |
| 501 | 錯誤. 這意味著同步驗證 **不** 支援此位置。 |
| 503 | 錯誤. 服務當前不可用。 客戶端應至少使用指數型回退策略重試三次。 |
