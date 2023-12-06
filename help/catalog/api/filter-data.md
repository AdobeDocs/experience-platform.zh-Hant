---
keywords: Experience Platform；首頁；熱門主題；篩選；篩選；篩選資料；日期範圍
solution: Experience Platform
title: 使用查詢引數篩選目錄資料
description: 目錄服務API可讓您透過使用請求查詢引數來篩選回應資料。 「目錄」最佳實務的一部分是在所有API呼叫中使用篩選器，因為它們會降低API的負載，並有助於改善整體效能。
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 75099d39fbdb9488105a9254bbbcca9b12349238
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 1%

---

# 篩選 [!DNL Catalog] 使用查詢引數的資料

此 [!DNL Catalog Service] API可讓您透過使用請求查詢引數來篩選回應資料。 最佳實務的一部分， [!DNL Catalog] 是在所有API呼叫中使用篩選器，因為它們會降低API的負載，並有助於改善整體效能。

本檔案會概述最常見的篩選方法 [!DNL Catalog] API中的物件。 建議您在閱讀 [目錄開發人員指南](getting-started.md) 以進一步瞭解如何與 [!DNL Catalog] API。 如需更多一般資訊，請參閱 [!DNL Catalog Service]，請參閱 [[!DNL Catalog] 概述](../home.md).

## 限制傳回的物件

此 `limit` 查詢引數會限制回應中傳回的物件數。 [!DNL Catalog] 會根據設定的限制自動計量回應：

* 如果 `limit` 未指定引數，每個回應裝載的物件數目上限為20。
* 針對資料集查詢，如果 `observableSchema` 是使用 `properties` 查詢引數，傳回的資料集數目上限為20。
* 所有其他目錄查詢的全域限製為100個物件。
* 無效 `limit` 引數(包括 `limit=0`)會產生400層級的錯誤回應，指出適當的範圍。
* 以查詢引數傳遞的限制或位移優先於以標頭傳遞的限制或位移。

**API格式**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 物件。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{LIMIT}` | 整數，表示傳回的物件數目，範圍從1到100。 |

**要求**

下列要求會擷取資料集清單，同時將回應限制在三個物件。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回資料集清單，數量限製為 `limit` 查詢引數。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## 限制顯示的屬性

即使使用篩選傳回的物件數 `limit` 引數，傳回的物件本身通常可包含比您實際需要更多的資訊。 若要進一步降低系統的負載，最佳實務是篩選回應，僅包含您需要的屬性。

此 `properties` 引數會篩選回應物件，以只傳回一組指定的屬性。 引數可以設定為傳回一或多個屬性。

此 `properties` 引數可以接受任何層級的物件屬性。 `sampleKey` 可使用以下專案擷取 `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 物件。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | 要包含在回應本文中的屬性名稱。 |
| `{OBJECT_ID}` | 特定專案的唯一識別碼 [!DNL Catalog] 正在擷取的物件。 |

**要求**

以下請求會擷取資料集清單。 以下提供的逗號分隔屬性名稱清單： `properties` 引數會指出回應中傳回的屬性。 A `limit` 也包含引數，這會限制傳回的資料集數目。 如果請求未包含 `limit` 引數，回應最多可包含20個物件。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回以下清單 [!DNL Catalog] 只顯示請求屬性的物件。

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

根據上述回應，可推斷出下列情況：

* 如果物件遺失任何要求的屬性，它只會顯示要求的屬性，但不包括它。(`Dataset1`)
* 如果物件不包含任何要求的屬性，則會顯示為空白物件。(`Dataset2`)
* 如果資料集包含屬性但沒有值，則該資料集可能會傳回請求的屬性作為空白物件。(`Dataset3`)
* 否則，資料集將顯示所有請求屬性的完整值。(`Dataset4`)

>[!NOTE]
>
>在 `schemaRef` 屬性中，版本號碼代表結構描述的最新次要版本。 請參閱以下小節： [方案版本設定](../../xdm/api/getting-started.md#versioning) XDM API指南以瞭解詳細資訊。

## 回應清單的位移開始索引

此 `start` 查詢引數會使用從零開始的編號，將回應清單向前位移指定的編號。 例如， `start=2` 會將回應位移，以便在列出的第三個物件上啟動。

如果 `start` 引數未與配對 `limit` 引數，傳回的物件數目上限為20。

**API格式**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要擷取的目錄物件型別。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OFFSET}` | 整數，表示要位移回應的物件數目。 |

**要求**

以下請求會擷取資料集清單，位移至第五個物件(`start=4`)並將回應限製為兩個傳回的資料集(`limit=2`)。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應包含的JSON物件包含兩個頂層專案(`limit=2`)，每個資料集各一個，其詳細資訊（範例中已壓縮詳細資訊）。 回應會偏移四點(`start=4`)，表示所示資料集依時間順序為第五和第六個。

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 依標籤篩選

有些目錄物件支援使用 `tags` 屬性。 標籤可以將資訊附加至物件，之後再用來擷取該物件。 您要使用哪些標籤以及如何套用這些標籤，取決於您的組織程式。

使用標籤時，需考量幾項限制：

* 目前支援標籤的目錄物件只有資料集、批次和連線。
* 標籤名稱對您的組織是唯一的。
* Adobe程式可能會針對特定行為利用標籤。 這些標籤的名稱會以「adobe」作為標準前置詞。 因此，宣告標籤名稱時，應避免此慣例。
* 以下標籤名稱保留供以下使用： [!DNL Experience Platform]，因此無法宣告為您的組織的標籤名稱：
   * `unifiedProfile`：此標籤名稱是保留給要內嵌的資料集 [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`：此標籤名稱是保留給要內嵌的資料集 [[!DNL Identity Service]](../../identity-service/home.md).

以下是包含下列專案的資料集範例： `tags` 屬性。 該屬性中的標籤會採取索引鍵值配對的形式，每個標籤值都會顯示為包含單一字串的陣列：

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

的值 `tags` 引數採用機碼值組的形式，使用格式 `{TAG_NAME}:{TAG_VALUE}`. 多個索引鍵/值組可以逗號分隔清單的形式提供。 提供多個標籤時，會假設AND關係。

引數支援萬用字元(`*`)作為標籤值。 例如，搜尋字串 `test*` 傳回標籤值開頭為「test」的任何物件。 僅由萬用字元組成的搜尋字串可用來根據物件是否包含特定標籤來篩選物件，無論其值為何。

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 物件。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 要作為篩選依據的標籤名稱。 |
| `{TAG_VALUE}` | 要作為篩選依據的標籤值。 支援萬用字元(`*`)。 |

**要求**

以下請求會擷取資料集清單，依具有特定值的標籤進行篩選，並顯示第二個標籤。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含的資料集清單 `sampleTag` 值為「123456」，並且 `secondTag` 具有任何值。 除非也指定限制，否則回應最多包含20個物件。

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
    }
}
```

## 依日期範圍篩選

中的某些端點 [!DNL Catalog] API的查詢引數允許範圍查詢，最常見的是日期查詢。

**API格式**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 參數 | 說明 |
| --- | --- |
| `{TIMESTAMP }` | 以Unix紀元時間為單位的日期時間整數。 |

**要求**

以下請求會擷取2019年4月期間建立的批次清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含清單 [!DNL Catalog] 在指定日期範圍內的物件。 除非也指定限制，否則回應最多包含20個物件。

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
    }
}
```

## 依屬性排序

此 `orderBy` 查詢引數可讓您根據指定的屬性值來排序（排序）回應資料。 此引數需要「direction」(`asc` 遞增或 `desc` （表示降序），後面接著冒號(`:`)，然後是排序結果的屬性。 如果未指定方向，預設方向會遞增。

能以逗號分隔的清單提供多個排序屬性。 如果第一個排序屬性產生多個物件，且這些物件包含該屬性的相同值，則會使用第二個排序屬性來進一步排序這些相符的物件。

例如，請考量下列查詢： `orderBy=name,desc:created`. 結果會根據第一個排序屬性以遞增順序排序。 `name`. 若有多個記錄共用相同專案 `name` 屬性，符合的記錄會依第二個排序屬性排序， `created`. 如果沒有傳回的記錄共用相同的 `name`，則 `created` 屬性不會納入排序的考量。


**API格式**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要擷取的目錄物件型別。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | 排序結果所依據的屬性名稱。 |

**要求**

下列請求會擷取按其排序的資料集清單 `name` 屬性。 如果任何資料集共用相同的 `name`，這些資料集將依次由其網站的 `updated` 屬性遞減排序。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含清單 [!DNL Catalog] 根據下列專案排序的物件： `orderBy` 引數。 除非也指定限制，否則回應最多包含20個物件。

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
    }
}
```

## 依屬性篩選

[!DNL Catalog] 提供兩種依屬性篩選的方法，以下幾節將進一步概述這些方法：

* [使用簡單篩選器](#using-simple-filters)：依特定屬性是否符合特定值篩選。
* [使用屬性引數](#using-the-property-parameter)：使用條件運算式來根據屬性是否存在，或如果屬性的值符合、接近或比較另一個指定值或規則運算式來篩選。

### 使用簡單篩選器 {#using-simple-filters}

簡單篩選器可讓您根據特定屬性值來篩選回應。 簡單篩選採用以下形式 `{PROPERTY_NAME}={VALUE}`.

例如，查詢 `name=exampleName` 只傳回物件，如果 `name` 屬性包含「exampleName」的值。 相反地，查詢 `name=!exampleName` 只傳回物件，如果 `name` 屬性為 **非** &quot;exampleName&quot;。

此外，簡單篩選器可支援查詢單一屬性的多個值。 提供多個值時，回應會傳回屬性相符的物件 **任何** 提供的清單中的值。 您可以藉由為多值查詢加上前置詞來反轉 `!` 字元至清單，只傳回屬性值為的物件 **非** 在提供的清單中(例如， `name=!exampleName,anotherName`)。

**API格式**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 物件。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | 您要用來篩選其值的屬性名稱。 |
| `{VALUE}` | 決定要包含（或排除，視查詢而定）之結果的屬性值。 |

**要求**

以下請求會擷取資料集清單，這些資料集經篩選後僅會包含 `name` 屬性的值為「exampleName」或「anotherName」。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含資料集清單，但不包括任何資料集 `name` 為「exampleName」或「anotherName」。 除非也指定限制，否則回應最多包含20個物件。

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
    }
}
```

### 使用 `property` 引數 {#using-the-property-parameter}

此 `property` 查詢引數比簡單篩選更能提供屬性型篩選的彈性。 除了依據屬性是否具備特定值進行篩選之外， `property` 引數可使用其他比較運運算元(例如「大於」(`>`)和「小於」(`<`))以及規則運算式，以依據屬性值篩選。 它也可以依屬性是否存在進行篩選，無論其值為何。

此 `property` 引數可以接受任何層級的物件屬性。 `sampleKey` 可用於篩選，使用 `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 物件。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | 指示要查詢的屬性以及如何評估其值的條件運算式。 範例如下。 |

的值 `property` 引數支援數種不同的條件運算式。 下表概述支援運算式的基本語法：

| 符號 | 說明 | 範例 |
| --- | --- | --- |
| （無） | 若不含運運算元而陳述屬性名稱，則只會傳回屬性存在的物件，無論其值為何。 | `property=name` |
| ！ | 加上「`!`」至的值 `property` 引數只會傳回屬性執行的物件 **非** 存在。 | `property=!name` |
| ~ | 只傳回屬性值（字串）符合波狀符號(`~`)符號。 | `property=name~^example` |
| == | 只傳回屬性值完全符合雙等符號(`==`)。 | `property=name==exampleName` |
| != | 只傳回屬性值具有下列特性的物件： **非** 不等於符號(`!=`)。 | `property=name!=exampleName` |
| &lt; | 只傳回屬性值小於（但不等於）指定數量的物件。 | `property=version<1.0.0` |
| &lt;= | 只傳回屬性值小於（或等於）指定數量的物件。 | `property=version<=1.0.0` |
| > | 只傳回屬性值大於（但不等於）指定數量的物件。 | `property=version>1.0.0` |
| >= | 只傳回屬性值大於（或等於）指定數量的物件。 | `property=version>=1.0.0` |

>[!NOTE]
>
>此 `name` 屬性支援使用萬用字元 `*`，當作整個搜尋字串或其中一部分。 萬用字元與空白字元相符，例如搜尋字串 `te*st` 會符合「test」值。 將星號加倍以逸出星號(`**`)。 搜尋字串中的雙星號代表單一星號為常值字串。

**要求**

下列請求將傳回版本號碼大於1.0.3的所有資料集。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含版本號大於1.0.3的資料集清單。除非也指定限制，否則回應最多包含20個物件。

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
    }
}
```

## 合併多個篩選器

使用&amp;符號(`&`)，您便可以在單一請求中合併多個篩選器。 將其他條件新增至請求時，假設為AND關係。

**API格式**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
