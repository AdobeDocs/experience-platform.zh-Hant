---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 串流區段
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 使用串流區段(Beta)即時評估事件

>[!NOTE] 串流區段是測試版功能，可應要求提供。

串流區段（也稱為連續查詢評估）是當事件進入特定區段群組時，立即評估客戶的能力。 有了這項功能，大部份的區段規則現在都可以在資料傳入Adobe Experience Platform時進行評估，這表示區段會籍會保持最新狀態，而不會執行排程的區段工作。

![](../images/api/streaming-segment-evaluation.png)

## 快速入門

本開發人員指南需要有效瞭解與串流細分相關的各種Adobe Experience Platform服務。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [即時客戶個人檔案](../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者個人檔案。
- [區段](../home.md):提供從即時客戶個人檔案資料建立細分和受眾的能力。
- [體驗資料模型(XDM)](../../xdm/home.md):平台組織客戶體驗資料的標準化架構。

以下章節提供您成功呼叫平台API所需的其他資訊。

### 讀取範例API呼叫

本開發人員指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

完成特定要求可能需要其他標題。 本檔案的每個範例都會顯示正確的標題。 請特別注意範例要求，以確保包含所有必要的標題。

### 啟用串流分段的查詢類型

下表列出不同類型的分段查詢，以及它們是否支援串流分段。

| 查詢類型 | 範例查詢 | 支援串流區段 |
| ---------- | ------------ | --------------------------------- |
| 簡單的人口統計 | 「把所有住址在加拿大的人都給我。」 | 支援 |
| 時間系列事件 | 「請給我所有下載Lightroom的人。」 | 支援 |
| 人口統計與時間系列 | 「請給我所有住在加拿大、在過去30天內下過訂單的人。」 | 支援 |
| 事件缺席 | &quot;給我兩天內放棄兩輛車的人。&quot; | 支援 |
| 多實體 | 「請給我所有權益類型為『有經驗』的人。」 | 不支援 |
| 高級PQL函式 | 「請提供我上週下單的所有描述檔，並包含所有購買產品的SKU和名稱。」 | 不支援 |

## 擷取所有啟用串流區段的區段

在建立新的可串流化區段或更新現有區段為可串流化之前，您應先擷取所有可串流化區段的清單，以確保您不會複製資訊。

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
  -H 'x-sandbox-name: {SANDBOX_NAME'
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

在確認您要建立的區段尚未存在後，您可以建立新區段，以啟用串流區段。

**API格式**

```http
POST /segment/definitions
```

**請求**

下列請求會建立啟用串流區段的新區段。 Note that the `continuous` section is set to `enabled: true`.

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

>[!NOTE] 這是標準的「建立區段」請求，區段的新增參 `continuous` 數會設為 `enabled: true`。 如需建立區段定義的詳細資訊，請參閱建立區段的 [檔案](../tutorials/create-a-segment.md)。

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

## 啟用現有的區段以進行串流區段

您可以在PATCH請求的路徑中提供區段定義的ID，以啟用現有區段進行串流分段。 此外，此PATCH請求的裝載必須包含現有段定義的完整詳細資訊，可通過對相關段定義發出GET請求來訪問該定義。

### 尋找現有的區段定義

若要尋找現有的區段定義，您必須在GET請求的路徑中提供其ID。

**API格式**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 您要尋找的區段定義ID。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回您所要求之區段定義的詳細資訊。

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "sandbox": {
        "sandboxId": "",
        "sandboxName": "",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    }
}
```

>[!NOTE] 對於下一個請求，您需要此回應中傳回之區段定義的完整詳細資訊。 請複製此回應的詳細資訊，以便用於下次請求的正文。

### 啟用現有的串流區段

現在您知道要更新的區段的詳細資訊，可以執行PATCH請求以更新區段，以啟用串流區段。

**API格式**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**請求**

下列請求的裝載會提供區段定義的詳細資訊(在上 [一步驟中取得](#look-up-an-existing-segment-definition))，並將其屬性變更 `continuous.enabled` 為更新 `true`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -d '{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
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

**回應**

成功的回應會傳回新更新之區段定義的詳細資料。

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "4A21D36B544916100A4C98A7@AdobeOrg",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
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
    },
    "creationTime": 1572029711000,
    "updateEpoch": 1572029712000,
    "updateTime": 1572029712000
}
```

## 啟用計畫評估

在啟用串流評估後，必須建立基準（在此之後區段將永遠是最新的）。 系統會自動執行此作業，但必須先啟用排程評估（也稱為排程分段），才能進行基線建立。

透過排程的分段，您的IMS組織可以建立循環排程，自動執行匯出工作以評估區段。

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
| `state` | *（可選）包含排程狀態的字串* 。 可用值： `active` 和 `inactive`。 預設值為 `inactive`. IMS組織只能建立一個排程。 本教學課程稍後將提供更新排程的步驟。 |

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

預設情況下，建立計畫時，除非將屬 `state` 性設定為建立(POST) `active` 請求主體中，否則該計畫處於非活動狀態。 通過向端點發出PATCH請求並在路徑中包 `state``active``/config/schedules` 括調度的ID，可以啟用調度（將設定為）。

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