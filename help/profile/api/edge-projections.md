---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Edge預測——即時客戶個人檔案API
topic: guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 2%

---


# 邊緣投影配置和目標端點

為即時跨多個通道為客戶提供協調、一致且個人化的體驗，需要隨時提供適當的資料，並在變更時持續更新。 Adobe Experience Platform可讓您透過使用所謂的邊緣，即時存取資料。 邊緣是地理位置優越的伺服器，可儲存資料，讓應用程式可輕鬆存取。 例如，Adobe Target和Adobe Campaign等Adobe應用程式會利用優勢，即時提供個人化客戶體驗。 資料通過投影被路由到邊，投影目的地定義資料要發送到的邊，投影配置定義將在邊上提供的特定資訊。 本指南提供使用 [!DNL Real-time Customer Profile] API處理邊緣投影的詳細指示，包括目標和設定。

## 快速入門

本指南中使用的API端點是 [[!DNL即時客戶配置檔案API]的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。 在繼續之前，請先閱讀快速入門 [指南](getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何 [!DNL Experience Platform] API所需之必要標題的重要資訊。

>[!NOTE]
>
>包含裝載(POST、PUT、PATCH)的請求需要標 `Content-Type` 頭。 本文檔中 `Content-Type` 使用了多個。 請特別注意範例呼叫中的標題，以確保您對每個請求都使 `Content-Type` 用正確。

## 投影目的地

通過指定要發送資料的位置，可將投影佈線到一個或多個邊。 建立的每個投影目標都有一個唯一ID，然後用於建立投影配置。

### 列出所有目標

您可以向端點發出GET請求，列出已為組織建立的邊緣目 `/config/destinations` 標。

**API格式**

```http
GET /config/destinations
```

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包括一個陣 `projectionDestinations` 列，每個目標的詳細資訊顯示為陣列內的單個對象。 如果尚未配置任何投影，則陣 `projectionDestinations` 列返回空。

>[!NOTE]
>
>此回應已縮短，僅顯示兩個目標。

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
| `_links.self.href` | 在頂層，與用於發出GET請求的路徑匹配。 在每個個別的目標物件中，此路徑可用於GET請求中，以直接查閱特定目標的詳細資料。 |
| `id` | 在每個目標對象中， `"id"` 顯示目標的唯讀、系統生成的唯一ID。 此ID用於引用特定目標和建立投影配置時。 |

有關個別目標屬性的詳細資訊，請參閱以下有關建 [立目標](#create-a-destination) 的章節。

### Create a destination {#create-a-destination}

如果所需的目標不存在，則可以通過向端點發出POST請求來建立新的投影目 `/config/destinations` 標。

**API格式**

```http
POST /config/destinations
```

**請求**

下列請求會建立新的邊緣目的地。

>[!NOTE]
>
>建立目的地的POST要求需要特定的標 `Content-Type` 題，如下所示。 使用錯誤 `Content-Type` 的標題會導致HTTP狀態415（不支援的媒體類型）錯誤。

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
| `type` **(必填)** | 要建立的目標類型。 唯一接受的值&quot;EDGE&quot;會建立邊緣目的地。 |
| `dataCenters` **(必填)** | 一個字串陣列，它列出要向其佈線投影的邊緣。 可包含下列一或多個值：「OR1」 —— 美國西部，「VA5」 —— 美國東部，「NLD1」 - EMEA。 |
| `ttl` **(必填)** | 指定投影有效期。 接受的值範圍：600至604800。 預設值：3600。 |
| `replicationPolicy` **(必填)** | 定義從集線器到邊緣的資料複製行為。  支援的值：主動、被動。 預設值：反應。 |

**回應**

成功的回應會傳回新建立之邊緣目的地的詳細資料，包括唯讀、系統產生的唯一ID(`id`)。

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
| `id` | 目標的唯讀、系統生成的唯一ID。 此ID用於直接和建立投影配置時引用目標。 |
| `version` | 此只讀值顯示目標的當前版本。 當目標更新時，版本號碼會自動增加。 |

### 檢視目標

如果您知道投影目的地的唯一ID，則可執行查閱請求以檢視其詳細資訊。 若要這麼做，請向端點提出GET請 `/config/destinations` 求，並在請求路徑中加入目標的ID。

**API格式**

```http
GET /config/destinations/{DESTINATION_ID}
```

| 參數 | 說明 |
|---|---|
| `{DESTINATION_ID}` | 您要檢視之投影目的地的唯一ID。 |

**請求**

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

響應對象顯示投影目標的詳細資訊。 屬 `id` 性應符合請求中提供之投影目的地的ID。

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

通過向端點發出PUT請求並在請求路 `/config/destinations` 徑中包括要更新的目標的ID，可以更新現有目標。 此操作實質上 _是重寫目標_ ，因此，在建立新目標時，必須在請求主體中提供與建立新目標相同的屬性。

>[!CAUTION]
>
>API對更新請求的回應是立即的，不過，對預測的變更會以非同步方式套用。 換言之，對目標的定義進行更新和應用更新之間存在時間差。

**API格式**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| 參數 | 說明 |
|---|---|
| `{DESTINATION_ID}` | 您要更新的投影目的地的唯一ID。 |

**請求**

下列請求會更新現有目的地以包含第二位置(`dataCenters`)。

>[!IMPORTANT]
>
>PUT請求需要特定的標 `Content-Type` 題，如下所示。 使用錯誤 `Content-Type` 的標題會導致HTTP狀態415（不支援的媒體類型）錯誤。

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
| `currentVersion` | 現有目標的當前版本。 執行目標查 `version` 閱請求時的屬性值。 |

**回應**

回應包含目標的更新詳細資料，包括其ID和目標 `version` 的新資訊。

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

如果您的組織不再需要投影目的地，則可透過向端點提出DELETE請求並在請求路徑中包含您要刪除之目的地的 `/config/destinations` ID來刪除它。

>[!CAUTION]
>
>刪除請求的API回應是立即回應，但是邊緣上資料的實際變更會非同步進行。 換言之，描述檔資料將從所有邊緣(在投影目的 `dataCenters` 地中指定)中移除，但處理將需要時間完成。

**API格式**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| 參數 | 說明 |
|---|---|
| `{DESTINATION_ID}` | 要刪除的投影目標的唯一ID。 |


**請求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

刪除請求會傳回HTTP狀態204（無內容）和空回應主體。 您可以透過依目標ID執行目標的查閱請求，確認刪除成功。 查閱應傳回HTTP狀態404（找不到）。

## 投影配置

投影配置提供了有關每個邊緣上應提供哪些資料的資訊。 投影不會將完 [!DNL Experience Data Model] 整(XDM)架構投影到邊緣，而只提供架構中的特定資料或欄位。 您的組織可以為每個XDM架構定義多個投影配置。

### 列出所有投影配置

通過向端點發出GET請求，可以列出為組織建立的所有投影配 `/config/projections` 置。 您也可以將可選參數新增至請求路徑，以存取特定方案的投影設定，或依其名稱查閱個別的投影。

**API格式**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| 參數 | 說明 |
|---|---|
| `{SCHEMA_NAME}` | 與要訪問的投影配置相關聯的方案類的名稱。 |
| `{PROJECTION_NAME}` | 要訪問的投影配置的名稱。 |

>[!NOTE]
>
>`schemaName` 是使用參數時的必 `name` 要值，因為投影配置名稱在模式類的上下文中是唯一的。

**請求**

以下請求列出與方案類關聯的所 [!DNL Experience Data Model] 有投影配置 [!DNL XDM Individual Profile]。 有關XDM及其在中的角色的更 [!DNL Platform]多資訊，請從閱讀 [XDM系統概述開始](../../xdm/home.md)。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回根屬性內包含在數 `_embedded` 組內的投影配置列 `projectionConfigs` 表。 如果沒有為您的組織進行投影配置，則陣 `projectionConfigs` 列將為空。

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

您可以建立(POST)新的投影配置，該配置將指定哪些XDM欄位可用於邊。

**API格式**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| 參數 | 說明 |
|---|---|
| `{SCHEMA_NAME}` | 與要訪問的投影配置相關聯的方案類的名稱。 |

**請求**

>[!NOTE]
>
>建立設定的POST要求需要特定的標 `Content-Type` 題，如下所示。 使用錯誤 `Content-Type` 的標題會導致HTTP狀態415（不支援的媒體類型）錯誤。

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
| `selector` | 一個字串，包含要複製到邊的方案內的屬性清單。 有關使用選擇器的最佳做法，請參閱本文 [檔的「選擇器](#selectors) 」部分。 |
| `name` | 新投影配置的描述性名稱。 |
| `destinationId` | 資料將投影至的邊緣目的地識別碼。 |

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

## Selectors {#selectors}

選擇器是以逗號分隔的XDM欄位名稱清單。 在投影配置中，選擇器指定要包括在投影中的屬性。 參數值的格 `selector` 式基於XPath語法鬆散。 支援的語法概述如下，並提供其他範例以供參考。

### 支援的語法

* 使用逗號來選取多個欄位。 因此請勿使用空格。
* 使用點符號來選取巢狀欄位。
   * 例如，要選擇一個名為的欄位， `field` 該欄位在名為的欄位中 `foo`嵌套，請使用選擇器 `foo.field`。
* 當包含包含子欄位的欄位時，所有子欄位也會依預設進行投影。 不過，您可以使用括弧來篩選傳回的子欄位 `"( )"`。
   * 例如， `addresses(type,city.country)` 僅返回每個陣列元素的地址類型和地址城市所在的 `addresses` 國家。
   * 上述範例等同於 `addresses.type,addresses.city.country`。

>[!NOTE]
>
>支援點記號和括弧記號來引用子欄位。 但是，使用點標籤法是最佳做法，因為它更簡明，並提供欄位階層的更佳圖示。

* 選取器中的每個欄位都會指定為回應的根。
   * 如果資料是資源的集合，則投影會包含資源陣列。
   * 如果資料是單一資源，則投影將包括與該資源相關的欄位。
   * 如果所選欄位是（或屬於）陣列，則投影將包括陣列中所有元素的選定部分。

### 選擇器參數的範例

以下範例顯示範 `selector` 例參數，後面接著它們所代表的結構化值。

**person.lastName**

返回所 `lastName` 請求資源中對 `person` 像的子欄位。

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**地址**

傳回陣列中的所 `addresses` 有元素，包括每個元素中的所有欄位，但不傳回其他欄位。

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

傳回 `person.lastName` 欄位和陣列中的所有 `addresses` 元素。

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
>每當傳回巢狀欄位時，投影就會包含封閉的父物件。 除非已明確選取父欄位，否則父欄位不包括任何其他子欄位。

**地址（類型，城市）**

僅傳回陣列中每 `type` 個元 `city` 素的和欄位值 `addresses` 。 每個元素中包含的所有其他子 `addresses` 欄位都被過濾掉。

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

本指南已向您顯示設定投影和目標所涉及的步驟，包括如何正確設定參數的格 `selector` 式。 您現在可以根據組織的需求建立新的投影目的地和設定。