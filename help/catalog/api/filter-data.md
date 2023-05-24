---
keywords: Experience Platform；首頁；熱門主題；過濾器；過濾器；過濾器；資料；過濾器；日期範圍
solution: Experience Platform
title: 使用查詢參數篩選目錄資料
description: 目錄服務API允許通過使用請求查詢參數篩選響應資料。 「目錄」的部分最佳做法是在所有API調用中使用篩選器，因為這些篩選器可減少API上的負載並幫助提高整體效能。
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 1%

---

# 篩選 [!DNL Catalog] 資料使用查詢參數

的 [!DNL Catalog Service] API允許通過使用請求查詢參數過濾響應資料。 最佳實踐的一部分 [!DNL Catalog] 是在所有API調用中使用篩選器，因為它們可減少API上的負載並幫助提高整體效能。

本文檔概述了篩選的最常用方法 [!DNL Catalog] 對象。 建議您在閱讀 [目錄開發人員指南](getting-started.md) 瞭解有關如何與 [!DNL Catalog] API。 有關 [!DNL Catalog Service]，請參見 [[!DNL Catalog] 概述](../home.md)。

## 限制返回的對象

的 `limit` 查詢參數約束在響應中返回的對象數。 [!DNL Catalog] 響應根據配置的限制自動計量：

* 如果 `limit` 未指定參數，每個響應負載的最大對象數為20。
* 對於資料集查詢，如果 `observableSchema` 是使用 `properties` 查詢參數，返回的資料集的最大數量為20。
* 所有其他目錄查詢的全局限制為100個對象。
* 無效 `limit` 參數(包括 `limit=0`)會導致400級錯誤響應，列出適當的範圍。
* 作為查詢參數傳遞的限制或偏移優先於作為標題傳遞的限制或偏移。

**API格式**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要檢索的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | 一個整數，表示要返回的對象數，範圍從1到100。 |

**要求**

以下請求將響應限制為三個對象時檢索資料集清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回資料集清單，該清單限於 `limit` 查詢參數。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## 限制顯示的屬性

即使在篩選使用 `limit` 參數時，返回的對象本身通常包含的資訊比實際需要的要多。 為了進一步減少系統上的負載，最佳做法是過濾響應，以僅包括您需要的屬性。

的 `properties` 參數篩選響應對象以僅返回一組指定的屬性。 可以將參數設定為返回一個或多個屬性。

的 `properties` 參數僅接受頂級對象屬性，這意味著對於以下示例對象，可以為 `name`。 `description`, `subItem`，但不是 `sampleKey`。

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API格式**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要檢索的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | 要包括在響應正文中的屬性的名稱。 |
| `{OBJECT_ID}` | 特定的唯一標識符 [!DNL Catalog] 正在檢索的對象。 |

**要求**

以下請求檢索資料集清單。 以逗號分隔的屬性名稱清單 `properties` 參數指示響應中要返回的屬性。 A `limit` 參數也包括在內，這將限制返回的資料集數。 如果請求未包括 `limit` 參數，響應最多包含20個對象。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回 [!DNL Catalog] 只顯示所請求屬性的對象。

```json
{
    "Dataset1": {
        "name": "Dataset 1",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/bc82c518380478b59a95c63e0f843121",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "Dataset2": {},
    "Dataset3": {
        "name": {},
    },
    "Dataset4": {
        "name": "Dataset 4",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

根據上述響應，可以推斷出：

* 如果對象缺少任何請求的屬性，則它將僅顯示其包含的請求屬性。(`Dataset1`)
* 如果對象不包括任何請求的屬性，則它將顯示為空對象。(`Dataset2`)
* 如果資料集包含屬性但沒有值，則該資料集可以將請求的屬性作為空對象返回。(`Dataset3`)
* 否則，資料集將顯示所有請求屬性的完整值。(`Dataset4`)

>[!NOTE]
>
>在 `schemaRef` 屬性，版本號表示架構的最新次版本。 請參閱 [架構版本](../../xdm/api/getting-started.md#versioning) 的子菜單。

## 響應清單的偏移起始索引

的 `start` 查詢參數使用基於零的編號將響應清單向前偏移指定的編號。 比如說， `start=2` 將抵消對第三個列出對象啟動的響應。

如果 `start` 參數與 `limit` 參數，返回的最大對象數為20。

**API格式**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要檢索的目錄對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | 一個整數，指示要將響應偏移的對象數。 |

**要求**

以下請求檢索資料集清單，偏移到第五個對象(`start=4`)和限制對兩個返回的資料集的響應(`limit=2`)。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

響應包括包含兩個頂級項的JSON對象(`limit=2`)，每個資料集和其詳細資訊各一個（在示例中已壓縮了詳細資訊）。 響應移四(`start=4`)，也就是說，所顯示的資料是按時間順序排列的5和6。

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 按標籤篩選

某些目錄對象支援使用 `tags` 屬性。 標籤可以將資訊附加到對象，然後稍後用於檢索該對象。 使用哪些標籤以及如何應用這些標籤的選擇取決於您的組織流程。

使用標籤時需要考慮以下幾個限制：

* 當前支援標籤的唯一目錄對象是資料集、批處理和連接。
* 標籤名稱對您的組織是唯一的。
* Adobe進程可能利用某些行為的標籤。 這些標籤的名稱以&quot;adobe&quot;作為標準前置詞。 因此，聲明標籤名稱時應避免此約定。
* 以下標籤名稱保留供跨 [!DNL Experience Platform]，因此不能聲明為組織的標籤名稱：
   * `unifiedProfile`:此標籤名稱保留用於要被攝取的資料集 [[!DNL Real-Time Customer Profile]](../../profile/home.md)。
   * `unifiedIdentity`:此標籤名稱保留用於要被攝取的資料集 [[!DNL Identity Service]](../../identity-service/home.md)。

下面是包含 `tags` 屬性。 該屬性中的標籤採用鍵值對的形式，每個標籤值都顯示為包含單個字串的陣列：

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{ORG_ID}",
        "tags": {
            "sampleTag": [
                "123456"
            ],
            "secondTag": [
                "sample_tag_value"
            ]
        },
        "name": "Sample Dataset",
        "description": "Same dataset containing sample data.",
        "dule": {
            "identity": [
                "I1"
            ]
        },
        "statsCache": {},
        "state": "DRAFT",
        "lastBatchId": "ca12b29612bf4052872edad59573703c",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "ca12b29612bf4052872edad59573703c",
        "namespace": "{NAMESPACE}",
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**API格式**

的值 `tags` 參數採用鍵值對的形式，使用 `{TAG_NAME}:{TAG_VALUE}`。 可以以逗號分隔清單的形式提供多個鍵值對。 當提供多個標籤時，假定為AND關係。

該參數支援通配符(`*`)。 例如， `test*` 返回標籤值以「test」開頭的任何對象。 僅由通配符組成的搜索字串可用於根據對象是否包含特定標籤（不管其值如何）來篩選對象。

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要檢索的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 要篩選依據的標籤的名稱。 |
| `{TAG_VALUE}` | 要篩選依據的標籤的值。 支援通配符(`*`)。 |

**要求**

以下請求檢索資料集清單，由具有特定值的一個標籤過濾，並且存在第二標籤。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含 `sampleTag` 值為&quot;123456&quot;, `secondTag` 值。 除非還指定了限制，否則響應最多包含20個對象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "Example tag value"
                ]
            },
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "A different tag value"
                ],
                "anotherTag": [
                    "2.0"
                ]
            },
            "dule": {},
            "statsCache": {}
    }
}
```

## 按日期範圍篩選

中的某些端點 [!DNL Catalog] API具有允許範圍查詢的查詢參數，在日期的情況下，這種查詢最常。

**API格式**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 參數 | 說明 |
| --- | --- |
| `{TIMESTAMP }` | Unix Epoch時間中的日期時間整數。 |

**要求**

以下請求檢索在2019年4月建立的批的清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包含 [!DNL Catalog] 位於指定日期範圍內的對象。 除非還指定了限制，否則響應最多包含20個對象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## 按屬性排序

的 `orderBy` query參數允許您根據指定的屬性值對響應資料進行排序（排序）。 此參數需要&quot;direction&quot;(`asc` 升序或 `desc` 對於降序)，後跟冒號(`:`)，然後是一個屬性，按排序結果。 如果未指定方向，則預設方向為升序。

可以在逗號分隔的清單中提供多個排序屬性。 如果第一個排序屬性生成包含該屬性相同值的多個對象，則第二個排序屬性將用於進一步對這些匹配對象進行排序。

例如，請考慮以下查詢： `orderBy=name,desc:created`。 根據第一個排序屬性， `name`。 在多個記錄共用相同的情況下 `name` 屬性，然後按第二個排序屬性對匹配記錄排序， `created`。 如果沒有返回的記錄共用相同 `name`，也請參見Wiki頁。 `created` 屬性不會影響排序。


**API格式**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要檢索的目錄對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 要按結果排序的屬性的名稱。 |

**要求**

以下請求檢索按其排序的資料集清單 `name` 屬性。 如果任何資料集共用相同 `name`這些資料集將依次按 `updated` 屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包含 [!DNL Catalog] 根據 `orderBy` 的下界。 除非還指定了限制，否則響應最多包含20個對象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## 按屬性篩選

[!DNL Catalog] 提供了兩種按屬性篩選的方法，這些方法在以下各節中進一步概述：

* [使用簡單篩選器](#using-simple-filters):按特定屬性是否與特定值匹配進行篩選。
* [使用屬性參數](#using-the-property-parameter):使用條件表達式根據屬性是否存在，或屬性的值是否與另一個指定值或規則運算式匹配、近似或比較進行篩選。

### 使用簡單篩選器 {#using-simple-filters}

通過簡單篩選器，可以根據特定屬性值篩選響應。 簡單過濾器採用 `{PROPERTY_NAME}={VALUE}`。

例如，查詢 `name=exampleName` 僅返回對象 `name` 屬性包含值「exampleName」。 相比之下，查詢 `name=!exampleName` 僅返回對象 `name` 屬性 **不** &quot;exampleName&quot;。

此外，簡單篩選器支援查詢單個屬性的多個值。 提供多個值時，響應將返回其屬性匹配的對象 **任何** 清單中的值。 可以通過預定 `!` 字元到清單，僅返回屬性值為 **不** 清單(例如， `name=!exampleName,anotherName`)。

**API格式**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要檢索的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 要篩選其值的屬性的名稱。 |
| `{VALUE}` | 一個屬性值，它確定要包括（或排除的結果，具體取決於查詢）。 |

**要求**

以下請求檢索資料集清單，篩選後只包括其 `name` 屬性的值為&quot;exampleName&quot;或&quot;atherName&quot;。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包含資料集清單，不包括其 `name` 是&quot;exampleName&quot;或&quot;athoreName&quot;。 除非還指定了限制，否則響應最多包含20個對象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

### 使用 `property` 參數 {#using-the-property-parameter}

的 `property` 與簡單篩選器相比，查詢參數為基於屬性的篩選提供了更大的靈活性。 除基於屬性是否具有特定值進行篩選外， `property` 參數可以使用其他比較運算子(如「多於」(`>`)和「小於」(`<`)以及按屬性值篩選的規則運算式。 它還可以通過屬性是否存在進行篩選，而不管其值如何。

的 `property` 參數只接受頂級對象屬性，這意味著對於以下示例對象，可以按屬性篩選 `name`。 `description`, `subItem`，但不是 `sampleKey`。

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API格式**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要檢索的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | 一個條件表達式，它指示要查詢的屬性以及如何計算其值。 下面提供了示例。 |

的值 `property` 參數支援多種不同的條件表達式。 下表概述了支援的表達式的基本語法：

| 符號 | 說明 | 範例 |
| --- | --- | --- |
| (None) | 聲明不帶運算子的屬性名稱只返回屬性存在的對象，而不考慮其值。 | `property=name` |
| ! | 預修&quot;`!`&quot;到 `property` 參數僅返回屬性所執行的對象 **不** 存在。 | `property=!name` |
| ~ | 僅返回其屬性值（字串）與在代號(`~`)。 | `property=name~^example` |
| == | 僅返回其屬性值與雙等於符號後提供的字串完全匹配的對象(`==`)。 | `property=name==exampleName` |
| != | 僅返回屬性值為 **不** 在not-equals符號(`!=`)。 | `property=name!=exampleName` |
| &lt; | 僅返回屬性值小於（但不等於）指定金額的對象。 | `property=version<1.0.0` |
| &lt;= | 僅返回其屬性值小於（或等於）規定金額的對象。 | `property=version<=1.0.0` |
| > | 僅返回其屬性值大於（但不等於）指定金額的對象。 | `property=version>1.0.0` |
| >= | 僅返回屬性值大於（或等於）指定金額的對象。 | `property=version>=1.0.0` |

>[!NOTE]
>
>的 `name` 屬性支援使用通配符 `*`，或作為整個搜索字串或作為搜索字串的一部分。 通配符與空字元匹配，因此搜索字串 `te*st` 將匹配值「test」。 將星號加倍以轉義(`**`)。 搜索字串中的雙星號表示作為文字字串的單星號。

**要求**

以下請求將返回版本號大於1.0.3的所有資料集。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包含版本號大於1.0.3的資料集清單。除非還指定了限制，否則響應最多包含20個對象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{ORG_ID}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{ORG_ID}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{ORG_ID}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## 合併多個篩選器

使用和號(`&`)，您可以在單個請求中組合多個篩選器。 當將附加條件添加到請求時，假定為AND關係。

**API格式**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
