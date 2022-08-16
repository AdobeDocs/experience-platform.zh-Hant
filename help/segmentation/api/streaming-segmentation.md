---
keywords: Experience Platform；主題；流行主題；分段；分段；分段服務；流分段；流分段；連續評價；
solution: Experience Platform
title: '基於流分割的近即時事件評估 '
topic-legacy: developer guide
description: 本文檔包含如何使用Adobe Experience Platform分段服務API進行流分段的示例。
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 654e141735b6882b4c0233b8e1c73d0838c8374e
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 1%

---

# 基於流分割的近即時事件評估

>[!NOTE]
>
>以下文檔說明如何使用API進行流分段。 有關使用UI使用流分段的資訊，請閱讀 [流分段UI指南](../ui/streaming-segmentation.md)。

流分段 [!DNL Adobe Experience Platform] 允許客戶在關注資料豐富度的同時進行近即時細分。 通過流分割，流資料進入時，段限定現在發生 [!DNL Platform]，緩解了調度和運行分段作業的需要。 使用此功能，現在可以在將資料傳遞到 [!DNL Platform]，這意味著段成員身份將保持最新，而不運行計畫的分段作業。

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>流分割對使用流源攝取的所有資料都有效。 使用基於批處理的源攝取的段將在夜間進行評估，即使它符合流分割的條件。
>
>此外，如果該段基於另一段，而該段是使用批分段進行評估的，則使用流分段評估的段可能在理想和實際隸屬度之間漂移。 例如，如果段A基於段B，並且使用批分段來評估段B，因為段B僅每24小時更新一次，則段A將進一步遠離實際資料，直到與段B更新重新同步。

## 快速入門

本開發人員指南要求對各種 [!DNL Adobe Experience Platform] 與流分割相關的服務。 在開始本教程之前，請查看以下服務的文檔：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個源的聚合資料即時提供統一的用戶配置檔案。
- [[!DNL Segmentation]](../home.md):提供從您的 [!DNL Real-time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

以下各節提供了您需要瞭解的其他資訊，以便成功撥打 [!DNL Platform] API。

### 讀取示例API調用

本開發人員指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

- 內容類型：應用程式/json

完成特定請求可能需要其他標頭。 本文檔中的每個示例都顯示了正確的標題。 請特別注意示例請求，以確保包含所有必需的標頭。

### 啟用流分段的查詢類型 {#query-types}

>[!NOTE]
>
>您需要為組織啟用計劃分段，以便流分段工作。 有關啟用計劃分段的資訊，請參閱 [啟用計劃分段](#enable-scheduled-segmentation)

為了使用流分段來評估段，該查詢必須符合以下准則。

| 查詢類型 | 詳細資訊 |
| ---------- | ------- |
| 單個事件 | 任何引用無時間限制的單個傳入事件的段定義。 |
| 相對時間窗口內的單個事件 | 任何引用單個傳入事件的段定義。 |
| 帶時間窗口的單個事件 | 任何段定義，它引用帶有時間窗口的單個傳入事件。 |
| 僅配置檔案 | 只引用配置檔案屬性的任何段定義。 |
| 具有配置檔案屬性的單個事件 | 任何引用單個傳入事件（無時間限制）和一個或多個配置檔案屬性的段定義。 **注：** 當事件發生時，將立即計算查詢。 但是，如果發生配置檔案事件，則必須等待24小時才能合併。 |
| 在相對時間窗口內具有配置檔案屬性的單個事件 | 任何引用單個傳入事件和一個或多個配置檔案屬性的段定義。 |
| 分部 | 包含一個或多個批或流段的任何段定義。 **注：** 如果使用段段，則會取消配置檔案資格 **每24小時**。 |
| 具有配置檔案屬性的多個事件 | 引用多個事件的任何段定義 **過去24小時內** 和（可選）具有一個或多個配置檔案屬性。 |

段定義將 **不** 在以下情形中啟用流分段：

- 段定義包括Adobe Audience Manager(AAM)段或特徵。
- 段定義包括多個實體（多實體查詢）。

請注意，執行流分段時應用以下准則：

| 查詢類型 | 准則 |
| ---------- | -------- |
| 單事件查詢 | 後視窗口沒有限制。 |
| 具有事件歷史記錄的查詢 | <ul><li>回望窗口限於 **一天**。</li><li>一個嚴格的時間排序條件 **必須** 存在於事件之間。</li><li>支援具有至少一個否定事件的查詢。 但是整個事件 **不能** 是否定。</li></ul> |

如果修改了段定義，使其不再滿足流分段的條件，則段定義將自動從「流」切換到「批」。

此外，與分段資格類似的分段取消資格會即時發生。 因此，如果聽眾不再有資格獲得某段節目，就會立即不合格。 例如，如果段定義要求「過去三小時內購買紅色鞋的所有用戶」，則在三小時後，最初符合段定義的所有配置檔案都將不合格。

## 檢索所有為流分段啟用的段

通過向IMS組織發出GET請求，您可以檢索IMS組織內所有支援流式分段的段的清單 `/segment/definitions` 端點。

**API格式**

要檢索啟用流式處理的段，必須包括查詢參數 `evaluationInfo.continuous.enabled=true` 的子菜單。

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

成功的響應將返回IMS組織中啟用流分段的陣列段。

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

## 建立啟用流式傳輸的段

如果段與其中一個 [上面列出的流分段類型](#query-types)。

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
    }
}'
```

>[!NOTE]
>
>這是標準的「建立段」請求。 有關建立段定義的詳細資訊，請閱讀有關 [建立段](../tutorials/create-a-segment.md)。

**回應**

成功的響應將返回新建立的啟用流式處理的段定義的詳細資訊。

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

## 啟用計畫評估 {#enable-scheduled-segmentation}

啟用流評估後，必須建立基線（在此之後段將始終保持最新）。 必須首先啟用計畫評估（也稱為計劃分段），以便系統自動執行基線。 通過計畫的分段，您的IMS組織可以遵循定期計畫自動運行導出作業以評估段。

>[!NOTE]
>
>可以為最多五(5)個合併策略的沙箱啟用計畫評估 [!DNL XDM Individual Profile]。 如果您的組織有五個以上的合併策略 [!DNL XDM Individual Profile] 在單個沙箱環境中，您將無法使用計畫的評估。

### 建立計畫

通過向 `/config/schedules` 端點，您可以建立調度並包括應觸發調度的特定時間。

**API格式**

```http
POST /config/schedules
```

**要求**

以下請求根據負載中提供的規範建立新調度。

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
| `name` | **（必需）** 計畫的名稱。 必須是字串。 |
| `type` | **（必需）** 作業類型為字串格式。 支援的類型包括 `batch_segmentation` 和 `export`。 |
| `properties` | **（必需）** 包含與計畫相關的其他屬性的對象。 |
| `properties.segments` | **(在 `type` 等於 `batch_segmentation`)** 使用 `["*"]` 確保包括所有段。 |
| `schedule` | **（必需）** 包含作業計畫的字串。 作業只能計畫為每天運行一次，這意味著您不能計畫在24小時內運行多次作業。 顯示的示例(`0 0 1 * * ?`)表示每天1時觸發作業:00:00 UTC。 如欲瞭解更多資訊，請查閱 [cron表達式格式](./schedules.md#appendix) 關於分段時間安排的檔案。 |
| `state` | *（可選）* 包含計畫狀態的字串。 可用值： `active` 和 `inactive`。 預設值為 `inactive`。IMS組織只能建立一個計畫。 本教程的後面部分提供了更新計畫的步驟。 |

**回應**

成功的響應將返回新建立的計畫的詳細資訊。

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

### 啟用計畫

預設情況下，建立計畫時處於非活動狀態，除非 `state` 屬性設定為 `active` 在建立(POST)請求正文中。 您可以啟用計畫(設定 `state` 至 `active`)，向PATCH請求 `/config/schedules` 端點，並在路徑中包括調度的ID。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**要求**

以下請求使用 [JSON修補程式格式](https://datatracker.ietf.org/doc/html/rfc6902) 以便更新 `state` 到 `active`。

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

成功更新將返回空的響應正文和HTTP狀態204（無內容）。

同一操作可用於禁用計畫，方法是將上一個請求中的「值」替換為「非活動」。

## 後續步驟

既然您為流分段啟用了新段和現有段，又啟用了計劃分段以開發基線並執行循環評估，您就可以開始為組織建立啟用流分段。

要瞭解如何使用Adobe Experience Platform用戶介面執行類似操作和使用段，請訪問 [段生成器使用手冊](../ui/segment-builder.md)。

## 附錄

以下部分列出了有關流分段的常見問題：

### 流切分是否也會即時發生「不合格」？

對於大多數情況，流分割的不合格是即時發生的。 但是，使用段段的流段確實 **不** 取消即時資格，而是在24小時後取消資格。

### 流分段處理的資料是什麼？

流分割對使用流源攝取的所有資料都有效。 使用基於批處理的源攝取的段將在夜間進行評估，即使它符合流分割的條件。 將在後續批處理作業中處理時間戳早於24小時流入系統的事件。

### 如何將段定義為批處理或流分段？

基於查詢類型和事件歷史持續時間的組合將段定義為批分段或流分段。 可在 [流式分段查詢類型節](#query-types)。

### 為什麼在「最後X天」下的「總合格」資料段數量在資料段詳細資訊部分中保持為零，而資料段數量卻繼續增加？

總合格段數從每日分段作業中提取，該作業包括符合批和流段資格的受眾。 此值將同時顯示批處理段和流式處理段。

「最後X天」下的數字 **僅** 包括符合流分段條件的受眾，以及 **僅** 如果已將資料流式傳輸到系統中，並且它計入流定義，則增加。 此值為 **僅** 顯示為流段。 因此，此值 **五月** 對於批段，顯示為0。

因此，如果您看到「最後X天」下的數字為零，並且線形圖也報告為零，則 **不** 將符合該段資格的任何配置檔案流入系統。