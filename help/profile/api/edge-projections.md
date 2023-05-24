---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 邊投影API端點
type: Documentation
description: Adobe Experience Platform使您能夠跨多個渠道即時地為客戶提供協調、一致和個性化的體驗，方法是讓適當的資料隨時可用，並隨著變化而不斷更新。 這是通過使用邊緣來完成的，邊緣是位於地理位置的伺服器，它儲存資料並使應用程式能夠方便地訪問資料。
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 2%

---

# 邊緣投影配置和目標端點

為了在多個渠道中為客戶提供協調、一致和個性化的即時體驗，需要隨時提供適當的資料並在發生更改時不斷更新。 Adobe Experience Platform通過使用所謂的邊緣實現對資料的即時訪問。 邊緣是位於地理位置的伺服器，它儲存資料，並使應用程式能夠方便地訪問資料。 例如，Adobe應用程式(如Adobe Target和Adobe Campaign)使用邊緣，以便即時提供個性化的客戶體驗。 資料通過投影被路由到邊緣，投影目的地定義要向其發送資料的邊緣，投影配置定義將在邊緣上提供的特定資訊。 本指南提供了使用 [!DNL Real-Time Customer Profile] 用於處理邊緣投影的API，包括目標和配置。

## 快速入門

本指南中使用的API終結點是 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)。 在繼續之前，請查看 [入門指南](getting-started.md) 有關指向相關文檔的連結、閱讀本文檔中示例API調用的指南，以及成功調用任何文檔所需的標題的重要資訊 [!DNL Experience Platform] API。

>[!NOTE]
>
>包含負載(POST、PUT、PATCH)的請求需要 `Content-Type` 標題。 多個 `Content-Type` 中。 請特別注意示例調用中的標頭，以確保您使用的是正確的 `Content-Type` 每個請求。

## 投影目標

通過指定要發送資料的位置，可將投影佈線到一個或多個邊。 建立的每個投影目標都具有唯一ID，然後該ID用於建立投影配置。

### 列出所有目標

您可以通過向以下站點發出GET請求，列出已為您的組織建立的邊緣目標 `/config/destinations` 端點。

**API格式**

```http
GET /config/destinations
```

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包括 `projectionDestinations` 陣列，每個目標的詳細資訊在陣列中顯示為單個對象。 如果尚未配置任何投影， `projectionDestinations` 陣列返回空。

>[!NOTE]
>
>此響應已縮短，僅顯示兩個目標。

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| 屬性 | 說明 |
|---|---|
| `_links.self.href` | 在頂層，匹配用於發出GET請求的路徑。 在每個單獨的目標對象內，此路徑可用於直接查找特定目標的詳細資訊的GET請求中。 |
| `id` | 在每個目標對象中， `"id"` 顯示目標的只讀、系統生成的唯一ID。 此ID用於引用特定目標和建立投影配置時。 |

有關單個目標屬性的詳細資訊，請參閱上 [建立目標](#create-a-destination) 接下來。

### 建立目標 {#create-a-destination}

如果所需的目標不存在，則可以通過向目標發出POST請求來建立新的投影目標 `/config/destinations` 端點。

**API格式**

```http
POST /config/destinations
```

**要求**

以下請求會建立新邊緣目標。

>[!NOTE]
>
>建立目標的POST請求需要特定 `Content-Type` 標題，如下所示。 使用錯誤 `Content-Type` 頭導致HTTP狀態415（不支援的媒體類型）錯誤。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

| 屬性 | 說明 |
|---|---|
| `type` **(必填)** | 要建立的目標類型。 唯一接受的值「EDGE」會建立邊緣目標。 |
| `dataCenters` **(必填)** | 一個字串陣列，列出要向其佈線投影的邊。 可能包含以下一個或多個值：&quot;OR1&quot; — 美國西部，&quot;VA5&quot; — 美國東部，&quot;NLD1&quot; - EMEA。 |
| `ttl` **(必填)** | 指定投影到期日。 接受值範圍：600到604800。 預設值：3600。 |
| `replicationPolicy` **(必填)** | 定義從集線器到邊緣的資料複製行為。  支援的值：主動，被動。 預設值：反應。 |

**回應**

成功的響應返回新建立的邊緣目標的詳細資訊，包括只讀、系統生成的唯一ID(`id`)。

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| 屬性 | 說明 |
|---|---|
| `self.href` | 此路徑用於直接查找(GET)目標，也可用於更新(PUT)或刪除(DELETE)目標。 |
| `id` | 目標的只讀、系統生成的唯一ID。 此ID用於直接引用目標並在建立投影配置時引用。 |
| `version` | 此只讀值顯示目標的當前版本。 更新目標後，版本號會自動遞增。 |

### 查看目標

如果您知道投影目標的唯一ID，則可以執行查找請求以查看其詳細資訊。 這是通過向 `/config/destinations` 端點，並包括請求路徑中目標的ID。

**API格式**

```http
GET /config/destinations/{DESTINATION_ID}
```

| 參數 | 說明 |
|---|---|
| `{DESTINATION_ID}` | 要查看的投影目標的唯一ID。 |

**要求**

以下請求執行查找(GET)以查看請求路徑中提供的ID的目標。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應對象顯示投影目標的詳細資訊。 的 `id` 屬性應與請求中提供的投影目標的ID匹配。

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### 更新目標

可通過向Web站點發出PUT請求來更新現有目標 `/config/destinations` 終結點，並包括要在請求路徑中更新的目標的ID。 此操作實質上是重寫目的地，因此在請求正文中必須提供與建立新目的地時提供的屬性相同的屬性。

>[!CAUTION]
>
>對更新請求的API響應是立即的，但是對預測的更改是非同步應用的。 換句話說，在對目標的定義進行更新和應用該定義之間存在時間差。

**API格式**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| 參數 | 說明 |
|---|---|
| `{DESTINATION_ID}` | 要更新的投影目標的唯一ID。 |

**要求**

以下請求更新現有目標以包括第二位置(`dataCenters`)。

>[!IMPORTANT]
>
>PUT請求需要 `Content-Type` 標題，如下所示。 使用錯誤 `Content-Type` 頭導致HTTP狀態415（不支援的媒體類型）錯誤。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| 屬性 | 說明 |
|---|---|
| `currentVersion` | 現有目標的當前版本。 的值 `version` 屬性。 |

**回應**

響應包括目標的更新詳細資訊，包括其ID和新 `version` 目的地。

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### 刪除目標

如果您的組織不再需要投影目標，則可以通過向 `/config/destinations` 端點，並在請求路徑中包括要刪除的目標的ID。

>[!CAUTION]
>
>對刪除請求的API響應是立即的，但是邊緣上資料的實際更改非同步發生。 換句話說，輪廓資料將從所有邊( `dataCenters` 在投影目標中指定)，但完成該過程需要時間。

**API格式**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| 參數 | 說明 |
|---|---|
| `{DESTINATION_ID}` | 要刪除的投影目標的唯一ID。 |


**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

刪除請求返回HTTP狀態204（無內容）和空響應正文。 您可以通過按目標ID對目標執行查找請求來確認刪除成功。 查找應返回HTTP狀態404（未找到）。

## 投影配置

投影配置提供了有關每個邊緣上應提供哪些資料的資訊。 而不是投影 [!DNL Experience Data Model] (XDM)模式到邊緣，投影只提供模式中的特定資料或欄位。 您的組織可以為每個XDM架構定義多個投影配置。

### 列出所有投影配置

您可以通過向以下站點發出GET請求，列出為組織建立的所有投影配置 `/config/projections` 端點。 您還可以向請求路徑添加可選參數以訪問特定方案的投影配置或按其名稱查找單個投影。

**API格式**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| 參數 | 說明 |
|---|---|
| `{SCHEMA_NAME}` | 與要訪問的投影配置關聯的架構類的名稱。 |
| `{PROJECTION_NAME}` | 要訪問的投影配置的名稱。 |

>[!NOTE]
>
>`schemaName` 使用 `name` 參數，因為投影配置名稱僅在架構類的上下文中唯一。

**要求**

以下請求列出了與 [!DNL Experience Data Model] 架構類， [!DNL XDM Individual Profile]。 有關XDM及其在 [!DNL Platform]，請從閱讀 [XDM系統概述](../../xdm/home.md)。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回根目錄內的投影配置清單 `_embedded` 屬性，包含在 `projectionConfigs` 陣列。 如果尚未為您的組織進行投影配置， `projectionConfigs` 陣列將為空。

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### 建立投影配置

可以建立(POST)新的投影配置，該配置將指示哪些XDM欄位在邊上可用。

**API格式**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| 參數 | 說明 |
|---|---|
| `{SCHEMA_NAME}` | 與要訪問的投影配置關聯的架構類的名稱。 |

**要求**

>[!NOTE]
>
>建立配置的POST請求需要特定 `Content-Type` 標題，如下所示。 使用錯誤 `Content-Type` 頭導致HTTP狀態415（不支援的媒體類型）錯誤。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| 屬性 | 說明 |
|---|---|
| `selector` | 一個字串，包含要複製到邊的架構內的屬性清單。 有關使用選擇器的最佳做法，請參見 [選擇器](#selectors) 的子菜單。 |
| `name` | 新投影配置的描述性名稱。 |
| `destinationId` | 資料將投影到的邊緣目標的標識符。 |

**回應**

成功的響應返回新建立的投影配置的詳細資訊。

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## 選擇器 {#selectors}

選擇器是XDM欄位名稱的逗號分隔清單。 在投影配置中，選擇器指定要包括在投影中的屬性。 格式 `selector` 參數值基於XPath語法鬆散。 下面概述了支援的語法，並提供了其他示例供參考。

### 支援的語法

* 使用逗號選擇多個欄位。 因此請勿使用空格。
* 使用點符號選擇嵌套欄位。
   * 例如，要選擇名為 `field` 嵌套在名為 `foo`，使用選擇器 `foo.field`。
* 如果包含包含子欄位的欄位，則預設情況下也會投影所有子欄位。 但是，可以使用括弧過濾返回的子欄位 `"( )"`。
   * 比如說， `addresses(type,city.country)` 僅返回每個地址的地址類型和地址所在的國家/地區 `addresses` 陣列元素。
   * 上例等效於 `addresses.type,addresses.city.country`。

>[!NOTE]
>
>對於引用子欄位，支援點記法和圓括弧記法。 但是，最好使用點記法，因為它更簡潔，而且更好地說明了欄位層次。

* 選擇器中的每個欄位都相對於響應的根指定。
   * 如果資料是資源集合，則投影將包括資源陣列。
   * 如果資料是單個資源，則投影將包括與該資源相關的欄位。
   * 如果所選欄位是（或是陣列的一部分），則投影將包括陣列中所有元素的選定部分。

### 選擇器參數示例

以下示例顯示示例 `selector` 參數，然後是它們所表示的結構化值。

**person.lastName**

返回 `lastName` 子欄位 `person` 請求資源中的對象。

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**地址**

返回中的所有元素 `addresses` 陣列，包括每個元素中的所有欄位，但沒有其他欄位。

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**person.lastName，地址**

返回 `person.lastName` 欄位中的所有元素 `addresses` 陣列。

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**地址.city**

僅返回地址陣列中所有元素的city欄位。

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>
>每當返回嵌套欄位時，投影就包括封閉的父對象。 除非也顯式選擇父欄位，否則父欄位不包括任何其他子欄位。

**地址（類型，城市）**

僅返回 `type` 和 `city` 中每個元素的欄位 `addresses` 陣列。 每個子欄位中包含的所有其他子欄位 `addresses` 元素被過濾掉。

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## 後續步驟

本指南向您展示了配置投影和目標所涉及的步驟，包括如何正確格式化 `selector` 的下界。 現在，您可以根據組織的需要建立新的投影目標和配置。
