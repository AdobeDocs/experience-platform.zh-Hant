---
keywords: Experience Platform；首頁；熱門主題；篩選；篩選；篩選資料；篩選資料；日期範圍
solution: Experience Platform
title: 使用查詢參數篩選目錄資料
description: 目錄服務API可透過使用要求查詢參數來篩選回應資料。 「目錄」的最佳實務是在所有API呼叫中使用篩選器，因為這些篩選器可減少API的負載，並有助於改善整體效能。
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 1%

---

# 篩選 [!DNL Catalog] 使用查詢參數的資料

此 [!DNL Catalog Service] API可透過使用要求查詢參數來篩選回應資料。 最佳作法的一部分 [!DNL Catalog] 是在所有API呼叫中使用篩選器，因為這些篩選器可減少API的負載，並有助於改善整體效能。

本檔案概述最常用的篩選方法 [!DNL Catalog] 物件。 建議您在閱讀 [目錄開發人員指南](getting-started.md) 進一步了解如何與 [!DNL Catalog] API。 有關 [!DNL Catalog Service]，請參閱 [[!DNL Catalog] 概述](../home.md).

## 限制返回的對象

此 `limit` 查詢參數會限制回應中傳回的物件數。 [!DNL Catalog] 根據設定的限制自動計量回應：

* 若 `limit` 參數，則每個回應裝載的物件數上限為20。
* 若是資料集查詢，若 `observableSchema` 是使用 `properties` 查詢參數中，傳回的資料集數上限為20。
* 所有其他目錄查詢的全域限制為100個物件。
* 無效 `limit` 參數(包括 `limit=0`)會導致400級錯誤回應，概述適當的範圍。
* 作為查詢參數傳遞的限制或偏移優先於作為標題傳遞的限制或偏移。

**API格式**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要擷取的物件。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | 一個整數，表示要返回的對象數，範圍從1到100。 |

**要求**

下列要求會在將回應限制為三個物件時，擷取資料集清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回資料集清單，但以 `limit` 查詢參數。

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

即使篩選使用 `limit` 參數，傳回的物件本身通常可包含您實際需要的更多資訊。 若要進一步降低系統的負載，最佳作法是篩選回應，僅包含您需要的屬性。

此 `properties` 參數會篩選回應物件，以僅傳回一組指定的屬性。 參數可設定為傳回一或多個屬性。

此 `properties` 參數僅接受頂層對象屬性，這表示對於以下示例對象，您可以為 `name`, `description`，和 `subItem`，但不適用於 `sampleKey`.

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
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要擷取的物件。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | 要包含在回應內文中的屬性名稱。 |
| `{OBJECT_ID}` | 特定的唯一識別碼 [!DNL Catalog] 要擷取的物件。 |

**要求**

下列請求會擷取資料集清單。 以下提供的以逗號分隔的屬性名稱清單： `properties` 參數會指出回應中要傳回的屬性。 A `limit` 也包含參數，這會限制傳回的資料集數量。 如果要求未包含 `limit` 參數，回應最多會包含20個物件。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回 [!DNL Catalog] 只顯示請求屬性的對象。

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

根據上述回應，可推斷出下列內容：

* 如果對象缺少任何請求的屬性，則它將只顯示它包含的請求屬性。(`Dataset1`)
* 如果對象不包括任何請求的屬性，則它將顯示為空對象。(`Dataset2`)
* 如果資料集包含屬性但沒有值，則可能會將請求的屬性傳回為空物件。(`Dataset3`)
* 否則，資料集會顯示所有請求屬性的完整值。(`Dataset4`)

>[!NOTE]
>
>在 `schemaRef` 屬性，版本編號會指出結構的最新次要版本。 請參閱 [方案版本設定](../../xdm/api/getting-started.md#versioning) （位於XDM API指南中）以取得詳細資訊。

## 響應清單的偏移起始索引

此 `start` 查詢參數使用零編號，將響應清單向前偏移指定的編號。 例如， `start=2` 會抵消第三個列出物件上開始的回應。

若 `start` 參數未與 `limit` 參數中，傳回的物件數上限為20。

**API格式**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要檢索的目錄對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | 一個整數，表示要偏移響應的對象數。 |

**要求**

下列請求會擷取資料集清單，並與第五個物件抵銷(`start=4`)和限制對兩個傳回資料集(`limit=2`)。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應包含JSON物件，其中包含兩個頂層項目(`limit=2`)、每個資料集及其詳細資訊各一個（範例中已壓縮詳細資訊）。 回應會移4(`start=4`)，表示顯示的資料集按時間順序為第5和第6個。

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 依標籤篩選

某些目錄物件支援使用 `tags` 屬性。 標籤可將資訊附加到對象，然後稍後用於檢索該對象。 要使用哪些標籤以及如何套用，取決於您的組織程式。

使用標籤時需考慮一些限制：

* 目前唯一支援標籤的目錄物件是資料集、批次和連線。
* 標籤名稱對您的IMS組織是唯一的。
* Adobe程式可能會針對特定行為使用標籤。 這些標籤的名稱會加上前置詞「adobe」作為標準。 因此，在聲明標籤名稱時應避免此慣例。
* 下列標籤名稱會保留供 [!DNL Experience Platform]，因此無法宣告為貴組織的標籤名稱：
   * `unifiedProfile`:此標籤名稱會保留給要擷取的資料集 [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`:此標籤名稱會保留給要擷取的資料集 [[!DNL Identity Service]](../../identity-service/home.md).

以下是包含 `tags` 屬性。 該屬性內的標籤會採取機碼值組的形式，每個標籤值會顯示為包含單一字串的陣列：

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

的值 `tags` 參數會採取機碼值組的形式，使用格式 `{TAG_NAME}:{TAG_VALUE}`. 能以逗號分隔清單的形式提供多個索引鍵值配對。 提供多個標籤時，會假設為AND關係。

參數支援萬用字元(`*`)（適用於標籤值）。 例如， `test*` 傳回標籤值以「test」開頭的任何物件。 僅由萬用字元組成的搜尋字串可用來根據物件是否包含特定標籤（無論其值為何）來篩選物件。

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要擷取的物件。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 要篩選依據的標籤名稱。 |
| `{TAG_VALUE}` | 要篩選的標籤值。 支援萬用字元(`*`)。 |

**要求**

下列請求會擷取資料集清單，依一個標籤進行篩選，其中一個標籤具有特定值，第二個標籤存在。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含的資料集清單 `sampleTag` 值為&quot;123456&quot;,AND `secondTag` 值。 除非另有指定限制，否則回應最多包含20個物件。

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

## 依日期範圍篩選

中的某些端點 [!DNL Catalog] API有查詢參數，可允許範圍查詢，在日期的情況下最常見。

**API格式**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 參數 | 說明 |
| --- | --- |
| `{TIMESTAMP }` | Unix Epoch時間中的日期時間整數。 |

**要求**

以下請求會擷取在2019年4月當月建立的批次清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含 [!DNL Catalog] 在指定日期範圍內的對象。 除非另有指定限制，否則回應最多包含20個物件。

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

此 `orderBy` 查詢參數可讓您根據指定的屬性值來排序（排序）回應資料。 此參數需要「方向」(`asc` 升序或 `desc` )，後面加上冒號(`:`)，然後是屬性來排序結果。 如果未指定方向，則預設方向為遞增方向。

以逗號分隔的清單可提供多個排序屬性。 如果第一個排序屬性生成多個對象，這些對象包含該屬性的相同值，則使用第二個排序屬性進一步排序那些匹配的對象。

例如，請考慮下列查詢： `orderBy=name,desc:created`. 根據第一個排序屬性，結果會以遞增順序排序。 `name`. 在多個記錄共用相同 `name` 屬性，則這些相符記錄會依第二個排序屬性排序， `created`. 如果沒有返回的記錄共用相同的 `name`, `created` 屬性不會納入排序中。


**API格式**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要檢索的目錄對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 要按結果排序的屬性名稱。 |

**要求**

下列請求會擷取依其排序的資料集清單 `name` 屬性。 如果有任何資料集共用相同 `name`，這些資料集的順序將依 `updated` 屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含 [!DNL Catalog] 根據 `orderBy` 參數。 除非另有指定限制，否則回應最多包含20個物件。

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

## 依屬性篩選

[!DNL Catalog] 提供兩種依屬性篩選的方法，以下各節將進一步概述：

* [使用簡單篩選](#using-simple-filters):依特定屬性是否符合特定值進行篩選。
* [使用屬性參數](#using-the-property-parameter):使用條件運算式來篩選，以判斷屬性是否存在，或是屬性的值是否符合、近似或與其他指定值或規則運算式比較。

### 使用簡單篩選 {#using-simple-filters}

簡單篩選可讓您根據特定屬性值來篩選回應。 簡單篩選會採取 `{PROPERTY_NAME}={VALUE}`.

例如，查詢 `name=exampleName` 僅返回對象 `name` 屬性包含「exampleName」值。 相反，查詢 `name=!exampleName` 僅返回對象 `name` 屬性為 **not** &quot;exampleName&quot;。

此外，簡單篩選器支援查詢單一屬性的多個值的功能。 提供多個值時，回應會傳回其屬性相符的物件 **any** 的值。 您可以借由預設 `!` 字元到清單，僅返回其屬性值為 **not** (例如， `name=!exampleName,anotherName`)。

**API格式**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要擷取的物件。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 要篩選其值的屬性名稱。 |
| `{VALUE}` | 一個屬性值，它根據查詢決定要包含（或排除）的結果。 |

**要求**

下列請求會擷取資料集清單（經過篩選），以僅包含其 `name` 屬性的值為「exampleName」或「otherName」。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含資料集清單，排除其 `name` 為&quot;exampleName&quot;或&quot;anotherName&quot;。 除非另有指定限制，否則回應最多包含20個物件。

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

此 `property` 與簡單篩選器相比，查詢參數可提供更大的屬性篩選彈性。 除了根據屬性是否具有特定值進行篩選外， `property` 參數可使用其他比較運算子(例如「更多」(`>`)和「小於」(`<`)，以及要依屬性值篩選的規則運算式。 它也可以依屬性是否存在進行篩選，無論其值為何。

此 `property` 參數僅接受頂層對象屬性，這表示對於以下示例對象，您可以按屬性篩選 `name`, `description`，和 `subItem`，但不適用於 `sampleKey`.

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
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要擷取的物件。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | 一個條件式運算式，指出要查詢的屬性，以及如何評估其值。 以下提供範例。 |

的值 `property` 參數支援數種不同的條件運算式。 下表概述支援運算式的基本語法：

| 符號 | 說明 | 範例 |
| --- | --- | --- |
| (None) | 聲明屬性名稱（不含運算子）只會傳回屬性存在的物件，而不論其值為何。 | `property=name` |
| ! | 前置詞「`!`&quot;到 `property` 參數僅返回屬性執行的對象 **not** 存在。 | `property=!name` |
| ~ | 僅傳回其屬性值（字串）符合在波狀符號(`~`)符號。 | `property=name~^example` |
| == | 僅傳回其屬性值與雙等號(`==`)。 | `property=name==exampleName` |
| != | 僅返回其屬性值的對象 **not** 在not-equals符號(`!=`)。 | `property=name!=exampleName` |
| &lt; | 僅傳回屬性值小於（但不等於）指定金額的物件。 | `property=version<1.0.0` |
| &lt;= | 僅返回其屬性值小於（或等於）指定量的對象。 | `property=version<=1.0.0` |
| > | 僅返回其屬性值大於（但不等於）指定量的對象。 | `property=version>1.0.0` |
| >= | 僅返回其屬性值大於（或等於）指定量的對象。 | `property=version>=1.0.0` |

>[!NOTE]
>
>此 `name` 屬性支援使用通配符 `*`，可作為整個搜尋字串或其中的一部分。 萬用字元符合空白字元，因此搜尋字串 `te*st` 會符合「test」值。 將星號加倍(`**`)。 搜尋字串中的雙星號代表單星號作為常值字串。

**要求**

下列請求會傳回版本編號大於1.0.3的所有資料集。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包含版本號大於1.0.3的資料集清單。除非另外指定限制，否則響應最多包含20個對象。

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

使用&amp;符號(`&`)，您可以在單一請求中合併多個篩選器。 將其他條件新增至請求時，會假設為AND關係。

**API格式**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
