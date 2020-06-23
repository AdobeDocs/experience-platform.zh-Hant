---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 串流區段
topic: developer guide
translation-type: tm+mt
source-git-commit: 822f43b139b68b96b02f9a5fe0549736b2524ab7
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 1%

---


# 使用串流分段功能，即時評估事件

透過串流分 [!DNL Adobe Experience Platform] 段功能，客戶可以近乎即時地進行分段，同時專注於資料的豐富性。 透過串流分段，區段資格現在會在資料進入時進行 [!DNL Platform]，減輕排程和執行分段工作的需求。 有了這項功能，大部份的區段規則現在都可以在資料傳入時進行評估 [!DNL Platform]，這表示區段成員資格將會保持最新，而不會執行排程的區段工作。

![](../images/api/streaming-segment-evaluation.png)

## 快速入門

本開發人員指南需要對串流細分相關的 [!DNL Adobe Experience Platform] 各種服務有良好的認識。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [!DNL Real-time Customer Profile](../../profile/home.md): 根據來自多個來源的匯總資料，即時提供統一的消費者個人檔案。
- [!DNL Segmentation](../home.md): 提供從資料建立區段和觀眾的 [!DNL Real-time Customer Profile] 能力。
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): 組織客戶體驗資料 [!DNL Platform] 的標準化架構。

以下章節提供您成功呼叫API所需的其他資訊 [!DNL Platform] 。

### 讀取範例API呼叫

本開發人員指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權： 生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型： application/json

完成特定要求可能需要其他標題。 本檔案的每個範例都會顯示正確的標題。 請特別注意範例要求，以確保包含所有必要的標題。

### 啟用串流分段的查詢類型 {#streaming-segmentation-query-types}

>[!NOTE] 您需要為組織啟用排程的分段，才能使串流分段正常運作。 如需啟用排程分段的詳細資訊，請參閱啟用排 [程分段區段一節](#enable-scheduled-segmentation)

若要使用串流分段來評估區段，查詢必須符合下列准則。

| 查詢類型 | 詳細資料 |
| ---------- | ------- |
| 傳入點擊 | 任何區段定義，是指沒有時間限制的單一傳入事件。 |
| 在相對時間視窗內傳入點擊 | 任何區段定義，是指過去七天內 **的單一傳入事件**。 |
| 參照描述檔的傳入點擊 | 任何區段定義，是指單一傳入事件（無時間限制）以及一或多個描述檔屬性。 |
| 在相對時間視窗內參照描述檔的傳入點擊 | 任何區段定義，是指過去七天內傳入的單一事件和一或多個描述 **檔屬性**。 |
| 參考描述檔的多個事件 | 任何區段定義是指過去24小時內 **的多個事件** ，且（可選）具有一或多個描述檔屬性。 |

下節列出區段定義範例，這些範例 **將無法** 針對串流區段啟用。

| 查詢類型 | 詳細資料 |
| ---------- | ------- | 
| 在相對時間視窗內傳入點擊 | 如果區段定義是指非在最 **近** 7天 **時段內的傳入事件**。 例如，在過去 **兩週內**。 |
| 參照相對視窗中描述檔的傳入點擊 | 下列選項將不 **支援串流** 區段：<ul><li>非在最 **近** 7天 **時段內傳入的事件**。</li><li>包含Adobe Audience Manager(AAM)區段或特徵的區段定義。</li></ul> |
| 參考描述檔的多個事件 | 下列選項將不 **支援串流** 區段：<ul><li>在過去24小 **時內** 未發 **生的事件**。</li><li>包含Adobe Audience Manager(AAM)區段或特徵的區段定義。</li></ul> |
| 多實體查詢 | 整體而言，串流分段不支 **援多** 實體查詢。 |

此外，執行串流區段時，也會套用一些准則：

| 查詢類型 | 准則 |
| ---------- | -------- |
| 單一事件查詢 | 回顧視窗限制為 **七天**。 |
| 具有事件歷史記錄的查詢 | <ul><li>回顧視窗限於一 **天**。</li><li>事件之間必須存 **在嚴格** 的時間順序條件。</li><li>僅允許事件之間的簡單時間順序（前後）。</li><li>無法否 **認個** 別事件。 不過，整個查詢 **可以** 否定。</li></ul> |

## 擷取所有啟用串流區段的區段

您可以透過向端點提出GET請求，擷取IMS組織內所有已啟用串流分段的區段 `/segment/definitions` 清單。

**API格式**

若要擷取啟用串流的區段，您必須在請求路徑中包 `evaluationInfo.continuous.enabled=true` 含查詢參數。

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

如果區段符合上列的其中一種串流區段類型，則會自 [動啟用串流](#streaming-segmentation-query-types)。

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

>[!NOTE] 這是標準的「建立區段」請求。 如需建立區段定義的詳細資訊，請閱讀建立區段 [的教學課程](../tutorials/create-a-segment.md)。

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

## 啟用計畫評估 {#enable-scheduled-segmentation}

在啟用串流評估後，必須建立基準（在此之後區段將永遠是最新的）。 必須先啟用計畫評估（也稱為計劃分段），系統才能自動執行基線。 透過排程的分段，您的IMS組織可以遵循循環排程，自動執行匯出工作以評估區段。

>[!NOTE] XDM個別設定檔的合併原則上限為五(5)個沙盒，可啟用排程的評估。 如果貴組織在單一沙盒環境中有5種以上的XDM個人設定檔合併原則，您將無法使用排程的評估。

### 建立排程

通過向端點發出POST請 `/config/schedules` 求，您可以建立調度並包括應觸發該調度的特定時間。

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
| `name` | **（必要）** ，排程名稱。 必須是字串。 |
| `type` | **（必要）** ，字串格式的工作類型。 支援的類型 `batch_segmentation` 為和 `export`。 |
| `properties` | **（必要）** ，包含與計畫相關的其他屬性的物件。 |
| `properties.segments` | **(等於時需`type`要`batch_segmentation`)** ：使用 `["*"]` 可確保包含所有區段。 |
| `schedule` | **（必要）** ，包含工作排程的字串。 作業只能排程為每天執行一次，這表示您無法排程作業在24小時期間執行多次。 顯示的範例(`0 0 1 * * ?`)意指每天在UTC 1:00:00觸發工作。 如需詳細資訊，請參閱 [cron運算式格式檔案](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 |
| `state` | *（可選）包含排程狀態的字串* 。 可用值： `active` 和 `inactive`。 預設值為 `inactive`。IMS組織只能建立一個排程。 本教學課程稍後將提供更新排程的步驟。 |

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

預設情況下，建立計畫時不活動，除非 `state` 在建立(POST)請 `active` 求主體中將屬性設定為。 通過向端點發出PATCH請求並在路徑中包 `state``active``/config/schedules` 括調度的ID，可以啟用調度（將設定為）。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**請求**

下列請求會使 [用JSON修補程式格式](http://jsonpatch.com/) ，以便將排程 `state` 更新為 `active`。

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

現在您已啟用新區段和現有區段的串流區段，並啟用排程區段來建立基準並執行循環評估，您就可以開始為組織建立區段。

若要瞭解如何使用Adobe Experience Platform使用者介面執行類似動作及使用區段，請造訪區段產生 [器使用指南](../ui/overview.md)。