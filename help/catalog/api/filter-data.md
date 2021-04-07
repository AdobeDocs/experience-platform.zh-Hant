---
keywords: Experience Platform;home；熱門主題；filter;Filter;filter data;filter data;date range
solution: Experience Platform
title: 使用查詢參數篩選目錄資料
topic: 開發人員指南
description: 目錄服務API允許透過使用請求查詢參數來篩選回應資料。 目錄的最佳實務是在所有API呼叫中使用篩選器，因為這些篩選器可減輕API的負載，並有助於改善整體效能。
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 1%

---

# 使用查詢參數篩選[!DNL Catalog]資料

[!DNL Catalog Service] API允許透過使用請求查詢參數來篩選回應資料。 [!DNL Catalog]的最佳實務是在所有API呼叫中使用篩選器，因為這些篩選器可降低API的負載，並有助於改善整體效能。

本檔案概述在API中篩選[!DNL Catalog]物件的最常用方法。 建議您在閱讀[目錄開發人員指南](getting-started.md)時參考本檔案，以進一步瞭解如何與[!DNL Catalog] API互動。 有關[!DNL Catalog Service]的更多一般資訊，請參見[[!DNL Catalog] overview](../home.md)。

## 限制返回的對象

`limit`查詢參數會限制回應中傳回的物件數目。 [!DNL Catalog] 回應會根據設定的限制自動計量：

* 如果未指定`limit`參數，則每個響應有效載荷的對象數上限為20。
* 對於資料集查詢，如果使用`properties`查詢參數請求`observableSchema`，則返回的資料集的最大數量為20。
* 所有其他目錄查詢的全局限制是100個對象。
* 無效的`limit`參數（包括`limit=0`）會導致400級錯誤回應，以列出正確的範圍。
* 作為查詢參數傳遞的限制或偏移優先於作為標題傳遞的限制或偏移。

**API格式**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要檢索的[!DNL Catalog]對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | 一個整數，表示要返回的對象數，範圍從1到100。 |

**請求**

下列請求會擷取資料集清單，同時限制對三個物件的回應。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回資料集清單，其數量僅限於`limit`查詢參數所指示的數量。

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

即使使用`limit`參數篩選傳回的物件數目，傳回的物件本身通常也會包含您實際需要的更多資訊。 為進一步降低系統的負載，最佳做法是篩選回應，只包含您所需的屬性。

`properties`參數篩選器只返回一組指定的屬性來響應對象。 參數可設為傳回一或多個屬性。

`properties`參數只接受頂層對象屬性，這表示對於以下示例對象，可以對`name`、`description`和`subItem`應用篩選器，但對`sampleKey`不能。

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
| `{OBJECT_TYPE}` | 要檢索的[!DNL Catalog]對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | 要包含在響應主體中的屬性的名稱。 |
| `{OBJECT_ID}` | 要檢索的特定[!DNL Catalog]對象的唯一標識符。 |

**請求**

下列請求會擷取資料集清單。 在`properties`參數下提供的屬性名稱的逗號分隔清單會指出要在回應中傳回的屬性。 也包含`limit`參數，可限制傳回的資料集數目。 如果請求未包含`limit`參數，則回應最多會包含20個物件。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回僅顯示所請求屬性的[!DNL Catalog]對象清單。

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

根據上述回應，可推斷出下列項目：

* 如果對象缺少任何請求的屬性，則它將只顯示它包含的請求屬性。(`Dataset1`)
* 如果對象不包含任何請求的屬性，則它將顯示為空對象。(`Dataset2`)
* 如果資料集包含屬性但沒有值，則可將請求的屬性傳回為空物件。(`Dataset3`)
* 否則，資料集會顯示所有請求屬性的完整值。(`Dataset4`)

>[!NOTE]
>
>在每個資料集的`schemaRef`屬性中，版本號表示架構的最新次要版本。 如需詳細資訊，請參閱XDM API指南中有關[架構版本控制](../../xdm/api/getting-started.md#versioning)的章節。

## 響應清單的偏移起始索引

`start`查詢參數使用零編號，將響應清單向前偏移指定的編號。 例如，`start=2`會偏移對第三個列出物件上開始的回應。

如果`start`參數未與`limit`參數配對，則返回的對象數上限為20。

**API格式**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要檢索的目錄對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | 一個整數，表示要偏移響應的對象數。 |

**請求**

以下請求檢索資料集清單，偏移到第五個對象(`start=4`)並限制對兩個返回資料集(`limit=2`)的響應。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應包含包含兩個頂層項目(`limit=2`)的JSON物件，每個資料集各有一個項目及其詳細資料（在範例中已壓縮詳細資料）。 回應會移四(`start=4`)，這表示顯示的資料集是按時間順序排列的五和六。

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 依標籤篩選

某些目錄對象支援使用`tags`屬性。 標籤可附加資訊至物件，然後稍後再用來擷取該物件。 要使用哪些標籤以及如何套用這些標籤的選擇取決於您的組織流程。

使用標籤時，需要考慮一些限制：

* 目前唯一支援標籤的目錄對象是資料集、批處理和連接。
* 標籤名稱是IMS組織唯一的。
* Adobe程式可能會針對某些行為使用標籤。 這些標籤的名稱會以&quot;adobe&quot;為前置詞作為標準。 因此，在聲明標籤名稱時，應避免此慣例。
* 下列標籤名稱會保留為供跨[!DNL Experience Platform]使用，因此無法宣告為組織的標籤名稱：
   * `unifiedProfile`:此標籤名稱保留給要被收錄的資料集 [[!DNL Real-time Customer Profile]](../../profile/home.md)。
   * `unifiedIdentity`:此標籤名稱保留給要被收錄的資料集 [[!DNL Identity Service]](../../identity-service/home.md)。

以下是包含`tags`屬性的資料集範例。 該屬性中的標籤採用鍵值配對的形式，每個標籤值顯示為包含單一字串的陣列：

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{IMS_ORG}",
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

`tags`參數的值採用鍵值對的形式，格式為`{TAG_NAME}:{TAG_VALUE}`。 可以以逗號分隔的清單形式提供多個鍵值對。 當提供多個標籤時，會假設AND關係。

此參數支援標籤值的萬用字元(`*`)。 例如，`test*`的搜尋字串會傳回任何標籤值以&quot;test&quot;開頭的物件。 僅由通配符組成的搜索字串可用於根據對象是否包含特定標籤（無論其值如何）來過濾對象。

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要檢索的[!DNL Catalog]對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 要篩選依據的標籤名稱。 |
| `{TAG_VALUE}` | 要篩選依據的標籤值。 支援萬用字元(`*`)。 |

**請求**

下列請求會擷取資料集的清單，依具有特定值的一個標籤進行篩選，而第二個標籤存在。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回包含值為&quot;123456&quot;的`sampleTag`和值為`secondTag`的資料集清單。 除非另有指定限制，否則回應最多包含20個物件。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

[!DNL Catalog] API中的某些端點具有允許區間查詢的查詢參數，在日期情況下最常見。

**API格式**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 參數 | 說明 |
| --- | --- |
| `{TIMESTAMP }` | Unix Epoch時間中的日期時間整數。 |

**請求**

以下請求會擷取在2019年4月建立的批清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含位於指定日期範圍內的[!DNL Catalog]物件清單。 除非另有指定限制，否則回應最多包含20個物件。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## 依屬性排序

`orderBy`查詢參數允許您根據指定的屬性值對響應資料進行排序（排序）。 此參數需要&quot;direction&quot;（`asc`代表遞增，`desc`代表遞減），後面接著冒號(`:`)，然後是屬性，以排序結果。 如果未指定方向，則預設方向為遞增。

可以在逗號分隔的清單中提供多個排序屬性。 如果第一個排序屬性生成多個對象，這些對象包含該屬性的相同值，則使用第二個排序屬性進一步排序這些匹配對象。

例如，請考慮以下查詢：`orderBy=name,desc:created`。 根據第一個排序屬性`name`，結果會以升序排序。 如果多個記錄共用相同的`name`屬性，則這些匹配記錄隨後按第二個排序屬性`created`排序。 如果沒有傳回的記錄共用相同的`name`，則`created`屬性不會納入排序。


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

**請求**

以下請求檢索按其`name`屬性排序的資料集清單。 如果任何資料集共用相同的`name` ，則這些資料集依其`updated`屬性的降序排列。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包含根據`orderBy`參數排序的[!DNL Catalog]對象清單。 除非另有指定限制，否則回應最多包含20個物件。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

[!DNL Catalog] 提供兩種依屬性篩選的方法，這些方法在下列章節中進一步概述：

* [使用簡單篩選](#using-simple-filters):依特定屬性是否符合特定值來篩選。
* [使用屬性參數](#using-the-property-parameter):使用條件運算式來篩選屬性是否存在，或屬性的值是否與其他指定值或規則運算式相符、相近或相比較。

### 使用簡單篩選器{#using-simple-filters}

簡單篩選可讓您根據特定屬性值來篩選回應。 簡單篩選器的形式為`{PROPERTY_NAME}={VALUE}`。

例如，查詢`name=exampleName`僅返回其`name`屬性包含&quot;exampleName&quot;值的對象。 相反地，查詢`name=!exampleName`只返回`name`屬性為&#x200B;**not** &quot;exampleName&quot;的對象。

此外，簡單篩選器支援查詢單一屬性之多個值的能力。 提供多個值時，響應返回屬性與提供清單中的值&#x200B;**any**&#x200B;匹配的對象。 您可以將`!`字元預先固定至清單，只傳回屬性值為&#x200B;**not**&#x200B;的物件（例如`name=!exampleName,anotherName`），以反轉多值查詢。

**API格式**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要檢索的[!DNL Catalog]對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 您要篩選其值的屬性名稱。 |
| `{VALUE}` | 一個屬性值，它決定要包括（或排除，視查詢而定）哪些結果。 |

**請求**

下列請求會擷取資料集的清單，篩選為僅包含`name`屬性值為&quot;exampleName&quot;或&quot;anotherName&quot;的資料集。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包含資料集清單，排除`name`為&quot;exampleName&quot;或&quot;anotherName&quot;的任何資料集。 除非另有指定限制，否則回應最多包含20個物件。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

### 使用`property`參數{#using-the-property-parameter}

與簡單篩選器相比，`property`查詢參數提供了更多基於屬性的篩選靈活性。 除了根據屬性是否具有特定值進行篩選外，`property`參數還可使用其他比較運算子(例如&quot;more-than&quot;(`>`)和&quot;less-than&quot;(`<`))以及規則運算式來依屬性值進行篩選。 它也可以依屬性是否存在來篩選，不論其值為何。

`property`參數只接受頂層對象屬性，這表示對於以下示例對象，可以按`name`、`description`和`subItem`的屬性進行篩選，但不能按`sampleKey`的屬性進行篩選。

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
| `{OBJECT_TYPE}` | 要檢索的[!DNL Catalog]對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | 一個條件式運算式，指出要查詢的屬性，以及如何評估其值。 以下提供範例。 |

`property`參數的值支援幾種不同的條件表達式。 下表概述支援運算式的基本語法：

| 符號 | 說明 | 範例 |
| --- | --- | --- |
| (None) | 聲明屬性名稱（不含運算子）時，只會傳回屬性存在的物件，不論其值為何。 | `property=name` |
| ! | 將&quot;`!`&quot;預定為`property`參數的值時，僅返回屬性&#x200B;**not**&#x200B;存在的對象。 | `property=!name` |
| ~ | 僅傳回屬性值（字串）與位元(`~`)符號後所提供的規則運算式相符的物件。 | `property=name~^example` |
| == | 僅返回其屬性值與雙等號(`==`)後提供的字串完全匹配的對象。 | `property=name==exampleName` |
| != | 僅傳回屬性值為&#x200B;**not**&#x200B;且符合在not-equals符號(`!=`)之後提供之字串的物件。 | `property=name!=exampleName` |
| &lt;> | 僅傳回屬性值小於（但不等於）指定金額的物件。 | `property=version<1.0.0` |
| &lt;> | 僅返回屬性值小於（或等於）指定金額的對象。 | `property=version<=1.0.0` |
| > | 僅傳回屬性值大於（但不等於）指定金額的物件。 | `property=version>1.0.0` |
| >= | 僅返回屬性值大於（或等於）指定金額的對象。 | `property=version>=1.0.0` |

>[!NOTE]
>
>`name`屬性支援使用萬用字元`*`作為整個搜尋字串或其一部分。 萬用字元會比對空字元，如此搜尋字串`te*st`就會比對值&quot;test&quot;。 星號加倍(`**`)即可逸出。 搜尋字串中的雙星號代表單一星號做為常值字串。

**請求**

以下請求將返回版本號大於1.0.3的任何資料集。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包含版本號大於1.0.3的資料集清單。除非另有指定限制，否則回應最多包含20個物件。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## 合併多個濾鏡

使用&amp;符號(`&`)，您可以在單一請求中組合多個篩選器。 當請求中新增其他條件時，會假設AND關係。

**API格式**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
