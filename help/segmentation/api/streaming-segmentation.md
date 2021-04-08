---
keywords: Experience Platform; home；熱門主題；分段；分段；分段服務；流分段；流分段；連續評價；
solution: Experience Platform
title: '使用串流分段功能，即時評估事件 '
topic: 開發人員指南
description: 本檔案包含如何搭配Adobe Experience Platform分段服務API使用串流分段的範例。
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
translation-type: tm+mt
source-git-commit: e1ae20412f449c991f53fdd0f095d0c3a6de262c
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 1%

---

# 使用串流分段功能，即時評估事件

>[!NOTE]
>
>下列檔案說明如何使用API使用串流分段。 有關使用UI使用串流分段的資訊，請閱讀[串流分段UI指南](../ui/streaming-segmentation.md)。

[!DNL Adobe Experience Platform]上的串流分段可讓客戶近乎即時地進行分段，同時專注於資料的豐富性。 透過串流分段，現在當串流資料進入[!DNL Platform]時，會進行分段資格設定，以減輕排程和執行分段工作的需求。 有了這項功能，現在可評估大部分區段規則，因為資料會傳入[!DNL Platform]，這表示區段成員資格會保持最新，而不會執行排程的區段工作。

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>串流區段只能用來評估串流至Platform的資料。 換言之，透過批次擷取所擷取的資料不會透過串流分段來評估，而且會與每夜排程的分段工作一起評估。

## 快速入門

本開發人員指南要求您對串流區段相關的各種[!DNL Adobe Experience Platform]服務有正確的瞭解。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者個人檔案。
- [[!DNL Segmentation]](../home.md):提供從資料建立區段和觀眾的 [!DNL Real-time Customer Profile] 能力。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

以下各節提供您必須知道的其他資訊，以便成功呼叫[!DNL Platform] API。

### 讀取範例API呼叫

本開發人員指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

完成特定要求可能需要額外的標題。 本檔案的每個範例都會顯示正確的標題。 請特別注意範例要求，以確保包含所有必要的標題。

### 啟用串流分段的查詢類型{#streaming-segmentation-query-types}

>[!NOTE]
>
>您需要為組織啟用排程的分段，才能使串流分段正常運作。 有關啟用計劃分段的資訊，請參閱[啟用計劃分段區段](#enable-scheduled-segmentation)

若要使用串流分段來評估區段，查詢必須符合下列准則。

| 查詢類型 | 詳細資料 |
| ---------- | ------- |
| 傳入點擊 | 任何區段定義，是指沒有時間限制的單一傳入事件。 |
| 在相對時間視窗內傳入點擊 | 任何參照單一傳入事件的區段定義。 |
| 含時間視窗的傳入點擊 | 任何區段定義，是指具有時間視窗的單一傳入事件。 |
| 僅限描述檔 | 任何僅指描述檔屬性的區段定義。 |
| 參照描述檔的傳入點擊 | 任何區段定義，是指單一傳入事件（無時間限制）以及一或多個描述檔屬性。 |
| 在相對時間視窗內參照描述檔的傳入點擊 | 任何區段定義，指單一傳入事件和一或多個描述檔屬性。 |
| 區段 | 包含一或多個批次或串流區段的任何區段定義。 |
| 參考描述檔的多個事件 | 在過去24小時內參照多個事件&#x200B;**且（可選）的區段定義具有一個或多個描述檔屬性。** |

在下列情況下，區段定義將&#x200B;**not**&#x200B;啟用串流區段：

- 區段定義包含Adobe Audience Manager(AAM)區段或特徵。
- 區段定義包括多個實體（多實體查詢）。

此外，執行串流區段時，也會套用一些准則：

| 查詢類型 | 准則 |
| ---------- | -------- |
| 單一事件查詢 | 回顧視窗沒有限制。 |
| 具有事件歷史記錄的查詢 | <ul><li>回顧視窗限制為&#x200B;**一天**。</li><li>事件之間存在嚴格的時間順序條件&#x200B;**必須**。</li><li>支援具有至少一個否定事件的查詢。 但是，整個事件&#x200B;**cannot**&#x200B;是否定。</li></ul> |

## 擷取所有啟用串流區段的區段

您可以向`/segment/definitions`端點提出GET請求，以擷取IMS組織內啟用串流分段的所有區段清單。

**API格式**

若要擷取啟用串流的區段，您必須在請求路徑中包含查詢參數`evaluationInfo.continuous.enabled=true`。

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**請求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回IMS組織中已啟用串流分段的區段陣列。

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## 建立可串流化的區段

如果區段符合上方所列的[串流區段類型之一，則會自動啟用串流。](#streaming-segmentation-query-types)

**API格式**

```http
POST /segment/definitions
```

**請求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

>[!NOTE]
>
>這是標準的「建立區段」請求。 如需建立區段定義的詳細資訊，請閱讀有關建立區段[的教學課程。](../tutorials/create-a-segment.md)

**回應**

成功的回應會傳回新建立的啟用串流的區段定義詳細資料。

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## 啟用計畫評估{#enable-scheduled-segmentation}

在啟用串流評估後，必須建立基準（在此之後區段將永遠是最新的）。 必須先啟用計畫評估（也稱為計劃分段），系統才能自動執行基線。 透過排程的分段，您的IMS組織可以遵循循環排程，自動執行匯出工作以評估區段。

>[!NOTE]
>
>對於[!DNL XDM Individual Profile]最多可啟用五(5)個合併策略的沙盒，可啟用計畫評估。 如果您的組織在單一沙盒環境中有超過5個[!DNL XDM Individual Profile]的合併原則，您將無法使用排程的評估。

### 建立排程

通過向`/config/schedules`端點發出POST請求，可以建立一個調度並包括應觸發該調度的特定時間。

**API格式**

```http
POST /config/schedules
```

**請求**

以下請求會根據裝載中提供的規格建立新的排程。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | **（必要）** 排程的名稱。必須是字串。 |
| `type` | **（必要）字** 串格式的作業類型。支援的類型有`batch_segmentation`和`export`。 |
| `properties` | **（必要）包** 含與計畫相關的其他屬性的物件。 |
| `properties.segments` | **(等於時需 `type` 要) `batch_segmentation`使** 用 `["*"]` 可確保包含所有區段。 |
| `schedule` | **（必要）包** 含工作排程的字串。作業只能排程為每天執行一次，這表示您無法排程作業在24小時期間執行多次。 顯示的示例(`0 0 1 * * ?`)表示每天在1:00:00 UTC觸發作業。 如需詳細資訊，請參閱[cron運算式格式](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)檔案。 |
| `state` | *（選用）包* 含排程狀態的字串。可用值：`active`和`inactive`。 預設值為 `inactive`。IMS組織只能建立一個排程。 本教學課程稍後將提供更新排程的步驟。 |

**回應**

成功的回應會傳回新建立之排程的詳細資料。

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### 啟用排程

預設情況下，建立計畫時將處於非活動狀態，除非在建立(POST)請求主體中將`state`屬性設定為`active`。 通過向`/config/schedules`端點發出PATCH請求並在路徑中包括調度的ID，可以啟用調度（將`state`設定為`active`）。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**請求**

以下請求使用[JSON修補程式格式](http://jsonpatch.com/)，以便將排程的`state`更新為`active`。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**回應**

成功的更新會傳回空回應主體和HTTP狀態204（無內容）。

使用相同的操作可以禁用調度，方法是將上一個請求中的&quot;value&quot;替換為&quot;inactive&quot;。

## 後續步驟

現在您已啟用新區段和現有區段的串流區段，並啟用排程區段以建立基準並執行循環評估，您就可以開始為組織建立可串流化的區段。

若要瞭解如何使用Adobe Experience Platform使用者介面執行類似動作及使用區段，請造訪[區段產生器使用指南](../ui/segment-builder.md)。
