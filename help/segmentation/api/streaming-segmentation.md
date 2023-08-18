---
solution: Experience Platform
title: 使用串流區段近乎即時地評估事件
description: 本檔案包含如何搭配Adobe Experience Platform Segmentation Service API使用串流區段的範例。
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 23504dd0909488e2ee63bf356fba4c7f0f7320dc
workflow-type: tm+mt
source-wordcount: '1956'
ht-degree: 1%

---

# 使用串流分段近乎即時地評估事件

>[!NOTE]
>
>以下檔案說明如何使用API串流分段。 如需有關使用UI使用串流區段的資訊，請參閱 [串流區段UI指南](../ui/streaming-segmentation.md).

串流區段於 [!DNL Adobe Experience Platform] 可讓客戶近乎即時進行細分，同時專注於資料豐富度。 有了串流區段，現在當串流資料進入時，就會進行區段資格 [!DNL Platform]，減少排程和執行分段工作的需求。 透過此功能，現在可以在資料傳入時評估大部分割槽段規則 [!DNL Platform]，表示區段會籍會保持最新狀態，而不會執行排程的區段工作。

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>串流區段適用於使用串流來源擷取的所有資料。 使用批次型來源擷取的區段將在夜間評估，即使它符合串流細分的資格。
>
>此外，如果區段定義是根據使用批次分段評估的另一個區段定義，則使用串流分段評估的區段定義可能會在理想成員資格和實際成員資格之間漂移。 例如，如果區段A是根據區段B，而區段B是使用批次分段進行評估的，由於區段B僅每24小時更新一次，因此區段A會與實際資料更遠，直到其與區段B更新重新同步為止。

## 快速入門

這份開發人員指南需要您實際瞭解各種 [!DNL Adobe Experience Platform] 串流細分涉及的服務。 在開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的消費者設定檔。
- [[!DNL Segmentation]](../home.md)：提供使用區段定義和其他外部來源建立對象的功能，來源為 [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。

以下小節提供您需瞭解的其他資訊，才能成功對進行呼叫 [!DNL Platform] API。

### 讀取範例API呼叫

本開發人員指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標題和正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有中每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 會隔離至特定的虛擬沙箱。 所有要求至 [!DNL Platform] API需要標頭，用以指定將進行作業的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

- Content-Type： application/json

可能需要額外的標頭才能完成特定請求。 本檔案的每個範例都會顯示正確的標題。 請特別留意範例要求，以確保包括所有必要的標頭。

### 已啟用串流區段的查詢型別 {#query-types}

>[!NOTE]
>
>您必須為組織啟用排程分段，串流分段才能運作。 有關啟用已排程分段的資訊，請參閱 [啟用已排程分段區段](#enable-scheduled-segmentation)

為了使用串流區段來評估區段定義，查詢必須符合以下准則。

| 查詢型別 | 詳細資訊 |
| ---------- | ------- |
| 單一事件 | 任何會參照沒有時間限制的單一傳入事件的區段定義。 |
| 相對時間範圍內的單一事件 | 任何參考單一傳入事件的區段定義。 |
| 具有時間範圍的單一事件 | 任何會參照具有時段之單一傳入事件的區段定義。 |
| 僅限設定檔 | 僅參考設定檔屬性的任何區段定義。 |
| 在少於24小時的相對時間範圍內，具有設定檔屬性的單一事件 | 任何區段定義，會參照具有一或多個設定檔屬性的單一傳入事件，且會在少於24小時的相對時間範圍內發生。 |
| 區段區段 | 包含一或多個批次或串流區段的任何區段定義。 **注意：** 如果使用區段區段，則會發生設定檔取消資格 **每24小時**. |
| 具有設定檔屬性的多個事件 | 任何參考多個事件的區段定義 **過去24小時內** 和（可選）有一或多個設定檔屬性。 |

區段定義會 **非** 在下列情況下啟用串流區段：

- 區段定義包含Adobe Audience Manager (AAM)區段或特徵。
- 區段定義包括多個實體（多實體查詢）。
- 區段定義包含單一事件和 `inSegment` 事件。
   - 但是，如果區段包含在 `inSegment` 事件只是設定檔，區段定義 **將** 已啟用串流區段。

請注意，進行串流細分時適用下列准則：

| 查詢型別 | 建議 |
| ---------- | -------- |
| 單一事件查詢 | 回顧期間沒有限制。 |
| 使用事件歷史記錄進行查詢 | <ul><li>回顧期間限製為 **一天**.</li><li>嚴格的時間排序條件 **必須** 存在於事件之間。</li><li>支援至少具有一個否定事件的查詢。 不過，整個事件 **無法** 是否定。</li></ul> |

如果區段定義經過修改，使其不再符合串流區段的條件，則區段定義會自動從「串流」切換為「批次」。

此外，區段取消資格（類似於區段資格）會即時發生。 因此，如果設定檔不再符合區段定義的資格，則會立即取消其資格。 例如，如果區段定義要求「過去三小時內購買紅鞋子的所有使用者」，三小時後，所有最初符合區段定義資格的設定檔都將不合格。

## 擷取為串流細分啟用的所有區段定義

您可以透過向「 」發出GET請求，擷取貴組織內為串流細分啟用的所有區段定義清單。 `/segment/definitions` 端點。

**API格式**

若要擷取已啟用串流的區段定義，您必須包含查詢引數 `evaluationInfo.continuous.enabled=true` 在請求路徑中。

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回組織中已啟用串流細分的一系列區段定義。

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

## 建立啟用串流的區段定義

如果區段定義符合以下其中一項，則會自動啟用串流功能： [上面列出的串流區段型別](#query-types).

**API格式**

```http
POST /segment/definitions
```

**要求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    }
}'
```

>[!NOTE]
>
>這是標準的「建立區段定義」請求。 如需建立區段定義的詳細資訊，請參閱以下教學課程： [建立區段定義](../tutorials/create-a-segment.md).

**回應**

成功的回應會傳回新建立的已啟用串流功能區段定義的詳細資料。

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
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

## 啟用排定的評估 {#enable-scheduled-segmentation}

啟用串流評估後，必須建立基準線（之後區段定義將一律為最新）。 排定的評估（也稱為排定的分段）必須先啟用，系統才能自動執行基準化。 透過已排程的分段，您的組織可以遵守週期性排程，自動執行匯出作業以評估區段定義。

>[!NOTE]
>
>對於最多有五(5)個合併原則的沙箱，可啟用排定的評估。 [!DNL XDM Individual Profile]. 如果貴組織擁有五個以上的合併原則 [!DNL XDM Individual Profile] 在單一沙箱環境中，您將無法使用排程的評估。

### 建立排程

POST藉由向 `/config/schedules` 端點，您可以建立排程並包含應觸發排程的特定時間。

**API格式**

```http
POST /config/schedules
```

**要求**

以下請求會根據承載中提供的規格建立新的排程。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | **（必要）** 排程的名稱。 必須為字串。 |
| `type` | **（必要）** 字串格式的工作型別。 支援的型別為 `batch_segmentation` 和 `export`. |
| `properties` | **（必要）** 包含與排程相關之其他屬性的物件。 |
| `properties.segments` | **(必要條件： `type` 等於 `batch_segmentation`)** 使用 `["*"]` 可確保納入所有區段定義。 |
| `schedule` | **（必要）** 包含工作排程的字串。 工作只能排程在一天執行一次，這表示您不能將工作排程在24小時內執行超過一次。 範例顯示為(`0 0 1 * * ?`)表示工作會在每天1點觸發:00:00 UTC。 如需詳細資訊，請參閱 [cron運算式格式](./schedules.md#appendix) 區段內排程的相關檔案內。 |
| `state` | *（可選）* 包含排程狀態的字串。 可用值： `active` 和 `inactive`. 預設值為 `inactive`。組織只能建立一個排程。 本教學課程稍後會介紹更新排程的步驟。 |

**回應**

成功的回應會傳回新建立排程的詳細資料。

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{ORG_ID}",
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

依預設，排程在建立時為非作用中，除非 `state` 屬性已設為 `active` 建立(POST)要求內文中。 您可以啟用排程(設定 `state` 至 `active`PATCH )，方式是向 `/config/schedules` 端點並在路徑中包含排程的ID。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**要求**

以下請求使用 [JSON修補程式格式](https://datatracker.ietf.org/doc/html/rfc6902) 以更新 `state` 至的排程 `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功更新會傳回空的回應本文和HTTP狀態204 （無內容）。

透過將先前請求中的「值」取代為「非作用中」，相同的作業可用於停用排程。

## 後續步驟

您現在已為串流細分啟用新的和現有的區段定義，並啟用排程細分以開發基準線並執行循環評估，您就可以開始為組織建立已啟用串流的區段定義。

若要瞭解如何使用Adobe Experience Platform使用者介面執行類似動作和使用區段定義，請造訪 [區段產生器使用手冊](../ui/segment-builder.md).

## 附錄

下節列出有關串流區段的常見問題：

### 串流區段「取消資格」也會即時發生嗎？

在大多數情況下，串流區段取消資格會即時發生。 不過，使用區段之串流區段定義的確會 **非** 即時取消資格，而不是在24小時後取消資格。

### 串流細分處理哪些資料？

串流區段適用於使用串流來源擷取的所有資料。 使用批次型來源擷取的區段將在夜間評估，即使它符合串流細分的資格。 時間戳記超過24小時的資料流進入系統的事件，將在後續批次作業中處理。

### 區段定義如何定義為批次或串流分段？

區段定義會根據查詢型別和事件歷史記錄持續時間的組合，定義為批次或串流分段。 若要列出哪些區段定義會評估為串流區段，請前往 [串流區段查詢型別區段](#query-types).

請注意，如果區段包含 **兩者** 一個 `inSegment` 運算式及直接單一事件鏈結，則不符合串流區段的資格。 如果您想要讓此區段定義符合串流細分的資格，您應該讓直接單一事件鏈結擁有自己的區段定義。

### 為什麼「合格」區段定義的數量持續增加，而「最近X天」下的數量在區段定義詳細資訊區段中仍維持零？

符合資格的區段定義總數是取自每日細分工作，其中包括同時符合批次和串流區段定義的對象。 批次和串流區段定義都會顯示此值。

「最近X天」下的數字 **僅限** 包含符合串流細分資格的對象，以及 **僅限** 如果您已將資料串流至系統，則會增加，而且會計入該串流定義。 此值為 **僅限** 顯示串流區段定義。 因此，這個值 **五月** 批次區段定義顯示為0。

因此，如果您看到「最近X天」底下的數字為零，而線圖也報告零，您會 **非** 已將任何符合該區段定義的設定檔串流至系統。

### 區段定義需要多久才能使用？

區段定義最多需要一小時才能使用。
