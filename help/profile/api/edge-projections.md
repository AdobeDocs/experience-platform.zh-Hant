---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 邊緣投影API端點
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform可讓您透過讓適當的資料隨時可用並持續更新，為跨多個管道的客戶即時提供協調、一致且個人化的體驗。 這是通過使用邊來完成的，邊是一個按地理位置放置的伺服器，它儲存資料，使應用程式可以輕鬆訪問。
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 4c544170636040b8ab58780022a4c357cfa447de
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 2%

---

# 邊緣投影設定和目標端點

為了即時為跨多個管道的客戶提供協調、一致且個人化的體驗，需要隨著變更隨時提供正確的資料並持續更新。 Adobe Experience Platform可透過使用所謂的Edge來即時存取資料。 邊緣是地理位置的伺服器，可儲存資料，讓應用程式可輕鬆存取。 例如，Adobe Target和Adobe Campaign等Adobe應用程式會使用Edge，以即時提供個人化的客戶體驗。 通過投影將資料路由到邊，投影目標定義要向其發送資料的邊，投影配置定義將在邊上提供的特定資訊。 本指南提供使用[!DNL Real-time Customer Profile] API處理邊緣投影的詳細指示，包括目的地和設定。

## 快速入門

本指南中使用的API端點是[[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 繼續之前，請檢閱[快速入門手冊](getting-started.md)，取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需的重要標題資訊。

>[!NOTE]
>
>包含裝載(POST、PUT、PATCH)的請求需要`Content-Type`標題。 本文檔中使用了多個`Content-Type`。 請特別注意範例呼叫中的標題，以確保您對每個請求使用正確的`Content-Type`。

## 投影目的地

通過指定要發送資料的位置，可以將投影佈線到一個或多個邊。 所建立的每個投影目標都有一個唯一ID，然後用於建立投影配置。

### 列出所有目的地

您可以向`/config/destinations`端點提出GET請求，以列出已為組織建立的邊緣目的地。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應包含`projectionDestinations`陣列，每個目的地的詳細資訊顯示為陣列內的個別物件。 如果未配置任何投影，`projectionDestinations`陣列將返回空。

>[!NOTE]
>
>此回應已縮短空間，只顯示兩個目的地。

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
| `_links.self.href` | 在頂層，會比對用來提出GET要求的路徑。 在每個個別目的地物件中，此路徑可用於GET請求，以直接查詢特定目的地的詳細資訊。 |
| `id` | 在每個目標對象中， `"id"`顯示目標的只讀、系統生成的唯一ID。 此ID用於參考特定目的地和建立投影設定時。 |

有關單個目標屬性的詳細資訊，請參閱以下關於建立目標](#create-a-destination)的部分。[

### 建立目的地 {#create-a-destination}

如果所需的目標尚未存在，則可以通過向`/config/destinations`端點發出POST請求來建立新的投影目標。

**API格式**

```http
POST /config/destinations
```

**要求**

下列請求會建立新的邊緣目的地。

>[!NOTE]
>
>建立目的地的POST請求需要特定的`Content-Type`標題，如下所示。 使用錯誤的`Content-Type`標題會導致HTTP狀態415（不支援的媒體類型）錯誤。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `type` **(必填)** | 要建立的目的地類型。 唯一接受的值「EDGE」會建立邊緣目的地。 |
| `dataCenters` **(必填)** | 列出要向其佈線投影的邊緣的字串陣列。 可包含下列一或多個值：&quot;OR1&quot; — 美國西部， &quot;VA5&quot; — 美國東部， &quot;NLD1&quot; - EMEA。 |
| `ttl` **(必填)** | 指定投影過期。 接受的值範圍：600至604800。 預設值：3600。 |
| `replicationPolicy` **(必填)** | 定義從集線器到邊緣的資料複製行為。  支援的值：主動，被動。 預設值：反應。 |

**回應**

成功的回應會傳回新建立之邊緣目的地的詳細資訊，包括唯讀、系統產生的唯一ID(`id`)。

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
| `self.href` | 此路徑可用於直接查找(GET)目的地，也可用於更新(PUT)或刪除(DELETE)目的地。 |
| `id` | 目的地的唯讀、系統產生的唯一ID。 此ID用於直接參照目標，以及建立投影配置時。 |
| `version` | 此唯讀值會顯示目的地的目前版本。 目標更新時，版本號碼會自動增加。 |

### 檢視目的地

如果您知道投影目的地的唯一ID，則可執行查詢請求以檢視其詳細資訊。 若要這麼做，請向`/config/destinations`端點提出GET要求，並在要求路徑中加入目的地的ID。

**API格式**

```http
GET /config/destinations/{DESTINATION_ID}
```

| 參數 | 說明 |
|---|---|
| `{DESTINATION_ID}` | 要查看的投影目標的唯一ID。 |

**要求**

下列請求會執行查閱(GET)，以檢視請求路徑中提供之ID的目的地。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應物件會顯示投影目的地的詳細資訊。 `id`屬性應符合要求中提供的投影目的地ID。

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

通過向`/config/destinations`端點發出PUT請求並在請求路徑中包括要更新的目標的ID，可以更新現有目標。 此操作實質上是重寫目標，因此，請求正文中必須提供與建立新目標時相同的屬性。

>[!CAUTION]
>
>更新要求的API回應會立即回應，不過，預測的變更會以非同步方式套用。 換言之，進行目標定義更新與套用目標定義之間的時間差異。

**API格式**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| 參數 | 說明 |
|---|---|
| `{DESTINATION_ID}` | 要更新的投影目標的唯一ID。 |

**要求**

下列請求會更新現有目的地以包含第二個位置(`dataCenters`)。

>[!IMPORTANT]
>
>PUT要求需要特定的`Content-Type`標題，如下所示。 使用錯誤的`Content-Type`標題會導致HTTP狀態415（不支援的媒體類型）錯誤。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `currentVersion` | 現有目的地的目前版本。 執行目標的查詢請求時的`version`屬性值。 |

**回應**

回應包含目標的更新詳細資訊，包括其ID和目標的新`version`。

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

### 刪除目的地

如果您的組織不再需要投影目的地，則可以透過向`/config/destinations`端點提出DELETE要求，並在要求路徑中加入您要刪除之目的地的ID，來刪除該目標。

>[!CAUTION]
>
>刪除請求的API回應會立即生效，不過Edge上資料的實際變更會非同步進行。 換句話說，將從所有邊（在投影目標中指定的`dataCenters`）中刪除輪廓資料，但該過程需要時間才能完成。

**API格式**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| 參數 | 說明 |
|---|---|
| `{DESTINATION_ID}` | 要刪除的投影目的地的唯一ID。 |


**要求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

刪除請求會傳回HTTP狀態204（無內容）和空的回應內文。 您可以依目的地的ID執行查詢請求，以確認刪除成功。 查閱應會傳回HTTP狀態404（找不到）。

## 投影配置

投影配置提供了關於每個邊緣上應提供哪些資料的資訊。 投影不會將完整的[!DNL Experience Data Model](XDM)架構投影到邊緣，而只會提供架構中的特定資料或欄位。 貴組織可為每個XDM結構定義多個投影設定。

### 列出所有投影配置

您可以向`/config/projections`端點提出GET請求，以列出為組織建立的所有投影配置。 您也可以將選用參數新增至請求路徑，以存取特定結構的投影設定，或依名稱查詢個別投影。

**API格式**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| 參數 | 說明 |
|---|---|
| `{SCHEMA_NAME}` | 與要訪問的投影配置相關聯的架構類的名稱。 |
| `{PROJECTION_NAME}` | 要訪問的投影配置的名稱。 |

>[!NOTE]
>
>`schemaName` 使用參數時為必 `name` 要值，因為投影配置名稱在架構類的上下文中是唯一的。

**要求**

以下請求列出與[!DNL Experience Data Model]架構類[!DNL XDM Individual Profile]關聯的所有投影配置。 有關XDM及其在[!DNL Platform]中的角色的詳細資訊，請從閱讀[ XDM系統概述](../../xdm/home.md)開始。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回`projectionConfigs`陣列中包含的根`_embedded`屬性內的投影配置清單。 如果尚未對您的組織進行投影配置，`projectionConfigs`陣列將為空。

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

您可以建立(POST)新的投影配置，以指定哪些XDM欄位可用於邊。

**API格式**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| 參數 | 說明 |
|---|---|
| `{SCHEMA_NAME}` | 與要訪問的投影配置相關聯的架構類的名稱。 |

**要求**

>[!NOTE]
>
>建立設定的POST請求需要特定的`Content-Type`標題，如下所示。 使用錯誤的`Content-Type`標題會導致HTTP狀態415（不支援的媒體類型）錯誤。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `selector` | 一個字串，其中包含要複製到Edge的架構內的屬性清單。 使用選取器的最佳實務可在本檔案的[選取器](#selectors)區段中取得。 |
| `name` | 新投影配置的描述性名稱。 |
| `destinationId` | 資料預計到的邊緣目的地識別碼。 |

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

## 選取器 {#selectors}

選取器是XDM欄位名稱的逗號分隔清單。 在投影配置中，選擇器指定要包含在投影中的屬性。 `selector`參數值的格式基於XPath語法鬆散。 支援的語法概述如下，並提供其他範例以供參考。

### 支援的語法

* 使用逗號來選取多個欄位。 因此請勿使用空格。
* 使用點記號來選取巢狀欄位。
   * 例如，要選擇名為`field`的欄位，該欄位嵌套在名為`foo`的欄位內，請使用選擇器`foo.field`。
* 包含包含子欄位的欄位時，預設情況下也會投影所有子欄位。 不過，您可以使用括弧`"( )"`來篩選傳回的子欄位。
   * 例如， `addresses(type,city.country)`僅針對每個`addresses`陣列元素返回地址類型和地址城市所在的國家/地區。
   * 上述範例等同於`addresses.type,addresses.city.country`。

>[!NOTE]
>
>參考子欄位支援點記號和括弧記號。 不過，使用點記號是最佳作法，因為它更精簡，並提供欄位階層的更佳圖示。

* 選取器中的每個欄位都是根據回應的根指定。
   * 如果資料是資源的集合，則投影將包含一個資源陣列。
   * 如果資料是單一資源，則投影將包含與該資源相對的欄位。
   * 如果所選欄位是陣列（或是陣列的一部分），則投影將包括陣列中所有元素的選定部分。

### 選取器參數的範例

下列範例顯示範例`selector`參數，及其代表的結構化值。

**person.lastName**

返回所請求資源中`person`對象的`lastName`子欄位。

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**地址**

傳回`addresses`陣列中的所有元素，包括每個元素中的所有欄位，但沒有其他欄位。

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

**person.lastName,addresses**

傳回`person.lastName`欄位和`addresses`陣列中的所有元素。

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

**addresses.city**

僅返回地址陣列中所有元素的城市欄位。

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
>每當返回嵌套欄位時，投影都包括封閉的父對象。 除非也明確選取父欄位，否則父欄位不包含任何其他子欄位。

**地址（類型，城市）**

僅傳回`addresses`陣列中每個元素的`type`和`city`欄位值。 每個`addresses`元素中包含的所有其他子欄位都被過濾掉。

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

本指南已示範設定投影和目的地的相關步驟，包括如何正確設定`selector`參數的格式。 您現在可以根據組織的需求建立新的投影目的地和設定。
