---
keywords: Experience Platform；首頁；熱門主題；篩選；篩選；篩選資料；日期範圍
solution: Experience Platform
title: 使用查詢引數篩選目錄資料
description: 使用查詢引數來篩選目錄服務API中的回應資料，並僅擷取您需要的資訊。 將篩選器套用至API呼叫，以降低負載並改善效能，確保更快且更有效率地擷取資料。
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 14ecb971af3f6cdcc605caa05ef6609ecb9b38fd
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 1%

---

# 使用查詢引數篩選[!DNL Catalog]資料

若要改善效能並擷取相關結果，請使用查詢引數來篩選[!DNL Catalog Service] API回應資料。

瞭解API中[!DNL Catalog]物件的常見篩選方法。 請將此檔案與[Catalog Developer Guide](getting-started.md)一併使用，以取得API互動的詳細資訊。 如需一般[!DNL Catalog Service]資訊，請參閱[[!DNL Catalog] 概觀](../home.md)。

## 限制傳回的物件 {#limit-returned-objects}

`limit`查詢引數會限制回應中傳回的物件數目。 [!DNL Catalog]個回應遵循預先定義的限制：

* 如果未指定`limit`引數，則每個回應的物件數目上限為20。
* 針對資料集查詢，如果使用`properties`查詢引數要求`observableSchema`，則傳回的資料集數目上限為20。
* 若為使用者權杖，上限為1。
* 對於服務權杖，最大限製為20。
* 其他目錄查詢的全域限製為100個物件。
* 無效的`limit`值（包括`limit=0`）導致400層級的錯誤回應，指定了適當的範圍。
* 作為查詢引數傳遞的限制或位移優先於標題中的限制或位移。

**API格式**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要擷取的[!DNL Catalog]物件型別。 有效物件： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{LIMIT}` | 指定傳回物件數目的整數（範圍： 1-100）。 |

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

成功的回應會傳回資料集清單，限制在`limit`查詢引數所指示的數量。

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

## 限制顯示的屬性 {#limit-displayed-properties}

即使使用`limit`引數篩選傳回的物件數目，傳回的物件本身通常也會包含超出您實際需要的更多資訊。 若要進一步降低系統的負載，最佳實務是篩選回應，僅包含您需要的屬性。

`properties`引數會篩選回應物件，以只傳回一組指定的屬性。 引數可以設定為傳回一或多個屬性。

`properties`引數可以接受任何層級的物件屬性。 可以使用`?properties=subItem.sampleKey`擷取`sampleKey`。

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
| `{OBJECT_TYPE}` | 要擷取的[!DNL Catalog]物件型別。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | 要包含在回應本文中的屬性名稱。 |
| `{OBJECT_ID}` | 正在擷取之特定[!DNL Catalog]物件的唯一識別碼。 |

**要求**

以下請求會擷取資料集清單。 在`properties`引數下提供的以逗號分隔的屬性名稱清單指示要在回應中傳回的屬性。 也包含`limit`引數，這會限制傳回的資料集數目。 如果要求不包含`limit`引數，回應最多將包含20個物件。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回[!DNL Catalog]物件清單，其中只顯示要求的屬性。

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
>在每個資料集的`schemaRef`屬性中，版本號碼會指出結構描述的最新次要版本。 如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../xdm/api/getting-started.md#versioning)的相關章節。

## 回應清單的位移開始索引 {#offset-starting-index}

`start`查詢引數會使用從零開始的編號，將回應清單向前位移指定的數字。 例如，`start=2`會將回應位移，以在列出的第三個物件上啟動。

如果`start`引數未與`limit`引數配對，則傳回的物件數目上限為20。

**API格式**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要擷取的目錄物件型別。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OFFSET}` | 整數，表示要位移回應的物件數目。 |

**要求**

下列要求會擷取資料集清單，將位移至第五個物件(`start=4`)，並將回應限製為兩個傳回的資料集(`limit=2`)。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應包含JSON物件，其中包含兩個頂層專案(`limit=2`)、每個資料集一個專案及其詳細資料（範例中已壓縮詳細資料）。 回應會偏移四(`start=4`)，表示顯示的資料集依時間順序為第五和第六位。

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 依標籤篩選

部分目錄物件支援使用`tags`屬性。 標籤可以將資訊附加至物件，之後再用來擷取該物件。 您要使用哪些標籤以及如何套用這些標籤，取決於您的組織程式。

使用標籤時，需考量幾項限制：

* 目前支援標籤的目錄物件只有資料集、批次和連線。
* 標籤名稱對您的組織是唯一的。
* Adobe程式可能會針對特定行為利用標籤。 這些標籤的名稱會以「adobe」作為標準前置詞。 因此，宣告標籤名稱時，應避免此慣例。
* 下列標籤名稱保留供[!DNL Experience Platform]使用，因此不能宣告為您的組織的標籤名稱：
   * `unifiedProfile`：此標籤名稱已保留給[[!DNL Real-Time Customer Profile]](../../profile/home.md)要內嵌的資料集。
   * `unifiedIdentity`：此標籤名稱已保留給[[!DNL Identity Service]](../../identity-service/home.md)要內嵌的資料集。

以下是包含`tags`屬性的資料集範例。 該屬性中的標籤會採取索引鍵值配對的形式，每個標籤值都會顯示為包含單一字串的陣列：

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

`tags`引數的值採用機碼值組的形式，使用格式`{TAG_NAME}:{TAG_VALUE}`。 多個索引鍵/值組可以逗號分隔清單的形式提供。 提供多個標籤時，會假設AND關係。

引數支援標籤值的萬用字元(`*`)。 例如，`test*`的搜尋字串會傳回標籤值以「test」開頭的任何物件。 僅由萬用字元組成的搜尋字串可用來根據物件是否包含特定標籤來篩選物件，無論其值為何。

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要擷取的[!DNL Catalog]物件型別。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li></ul> |
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

成功的回應會傳回資料集清單，該資料集包含值為「123456」的`sampleTag`以及任何值的`secondTag`。 除非也指定限制，否則回應最多包含20個物件。

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

[!DNL Catalog] API中某些端點的查詢引數允許範圍查詢，最常見的是日期查詢。

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

成功的回應包含指定日期範圍內的[!DNL Catalog]物件清單。 除非也指定限制，否則回應最多包含20個物件。

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

`orderBy`查詢引數可讓您根據指定的屬性值來排序（排序）回應資料。 此引數需要「方向」（`asc`為遞增或`desc`為遞減），後面接著冒號(`:`)，然後是排序結果的屬性。 如果未指定方向，預設方向會遞增。

能以逗號分隔的清單提供多個排序屬性。 如果第一個排序屬性產生多個物件，且這些物件包含該屬性的相同值，則會使用第二個排序屬性來進一步排序這些相符的物件。

例如，請考量下列查詢： `orderBy=name,desc:created`。 結果會根據第一個排序屬性`name`以遞增順序排序。 如果有多個記錄共用相同的`name`屬性，則這些相符的記錄會依第二個排序屬性`created`排序。 如果沒有傳回的記錄共用相同的`name`，則`created`屬性不會納入排序中。


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

下列請求會擷取按資料集`name`屬性排序的資料集清單。 如果任何資料集共用相同的`name`，這些資料集將依次按其`updated`屬性以降序排序。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含根據`orderBy`引數排序的[!DNL Catalog]物件清單。 除非也指定限制，否則回應最多包含20個物件。

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

[!DNL Catalog]提供兩種依屬性篩選的方法，以下幾節將對這些方法做進一步概述：

* [使用簡單篩選器](#using-simple-filters)：依特定屬性是否符合特定值來篩選。
* [使用屬性引數](#using-the-property-parameter)：使用條件運算式來篩選屬性是否存在，或屬性的值是否符合、近似或與其他指定值或規則運算式比較。

>[!NOTE]
>
>目錄物件的任何屬性都可用於篩選目錄服務API中的結果。

### 使用簡單篩選器 {#using-simple-filters}

簡單篩選器可讓您根據特定屬性值來篩選回應。 簡單篩選器採用`{PROPERTY_NAME}={VALUE}`的形式。

例如，查詢`name=exampleName`只傳回`name`屬性包含「exampleName」值的物件。 相較之下，查詢`name=!exampleName`只傳回`name`屬性為&#x200B;**而非** &quot;exampleName&quot;的物件。

此外，簡單篩選器可支援查詢單一屬性的多個值。 提供多個值時，回應會傳回其屬性符合所提供清單中&#x200B;**any**&#x200B;個值的物件。 您可以在清單中加上`!`字元前置詞，以反轉多值查詢，只傳回所提供清單中屬性值為&#x200B;**而非**&#x200B;的物件（例如`name=!exampleName,anotherName`）。

**API格式**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要擷取的[!DNL Catalog]物件型別。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | 您要用來篩選其值的屬性名稱。 |
| `{VALUE}` | 決定要包含（或排除，視查詢而定）之結果的屬性值。 |

**要求**

下列請求會擷取資料集清單，經篩選後僅納入其`name`屬性值為「exampleName」或「anotherName」的資料集。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含資料集清單，排除`name`為「exampleName」或「anotherName」的任何資料集。 除非也指定限制，否則回應最多包含20個物件。

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

### 使用`property`引數 {#using-the-property-parameter}

`property`查詢引數比簡單篩選提供更大的彈性以屬性為基礎的篩選。 除了根據屬性是否具有特定值來進行篩選之外，`property`引數還可以使用其他比較運運算元(例如「大於」(`>`)和「小於」(`<`))以及規則運算式來依屬性值進行篩選。 它也可以依屬性是否存在進行篩選，無論其值為何。

使用&amp;符號(`&`)來結合多個篩選器，並在單一請求中精簡您的查詢。 依多個欄位篩選時，預設會套用`AND`關係。

>[!NOTE]
>
>若您在單一查詢中合併多個`property`引數，則必須至少將一個引數套用至`id`或`created`欄位。 下列查詢傳回`id`為`abc123` **且** `name`不是`test`的物件：
>
>```http
>GET /datasets?property=id==abc123&property=name!=test
>```

如果您在同一欄位上使用多個`property`引數，則只有最後指定的引數才會生效。

>[!IMPORTANT]
>
>您&#x200B;**無法**&#x200B;使用單一`property`引數一次篩選多個欄位。 每個欄位都必須有自己的`property`引數。 下列範例(`property=id>abc,name==myDataset`)是&#x200B;**不允許**，因為它嘗試在&#x200B;**單一`property`引數**&#x200B;中套用條件至`id`和`name`。

`property`引數可以接受任何層級的物件屬性。 `sampleKey`可以使用`?properties=subItem.sampleKey`進行篩選。

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
| `{OBJECT_TYPE}` | 要擷取的[!DNL Catalog]物件型別。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | 指示要查詢的屬性以及如何評估其值的條件運算式。 範例如下。 |

`property`引數的值支援數種不同的條件運算式。 下表概述支援運算式的基本語法：

| 符號 | 說明 | 範例 |
| --- | --- | --- |
| （無） | 若不含運運算元而陳述屬性名稱，則只會傳回屬性存在的物件，無論其值為何。 | `property=name` |
| ！ | 將&quot;`!`&quot;前置詞設為`property`引數的值，只會傳回屬性&#x200B;**不**&#x200B;存在的物件。 | `property=!name` |
| ~ | 只傳回屬性值（字串）符合在波狀符號(`~`)後面提供的規則運算式的物件。 | `property=name~^example` |
| == | 只傳回其屬性值完全符合雙等號(`==`)之後提供的字串的物件。 | `property=name==exampleName` |
| ！= | 只傳回屬性值不符合&#x200B;**不**&#x200B;和不等於符號(`!=`)後面提供的字串的物件。 | `property=name!=exampleName` |
| &lt; | 只傳回屬性值小於（但不等於）指定數量的物件。 | `property=version<1.0.0` |
| &lt;= | 只傳回屬性值小於（或等於）指定數量的物件。 | `property=version<=1.0.0` |
| > | 只傳回屬性值大於（但不等於）指定數量的物件。 | `property=version>1.0.0` |
| >= | 只傳回屬性值大於（或等於）指定數量的物件。 | `property=version>=1.0.0` |
| * | 萬用字元會套用至任何字串屬性，並符合任何字元順序。 使用`**`來逸出常值星號。 | `property=name==te*st` |
| &amp; | 結合多個`property`引數以及它們之間的`AND`關係。 | `property=id==abc&property=name!=test` |

>[!NOTE]
>
>`name`屬性支援使用萬用字元`*`，做為整個搜尋字串或其中一部分。 萬用字元與空白字元相符，因此搜尋字串`te*st`會符合「test」值。 將星號加倍(`**`)以逸出星號。 搜尋字串中的雙星號代表單一星號為常值字串。

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

## 使用屬性引數篩選陣列 {#filter-arrays}

根據陣列屬性篩選結果時，請使用相等和不等運運算元來包含或排除特定值。

### 相等篩選器 {#equality-filters}

若要依多個值篩選陣列欄位，請對每個值使用個別的屬性引數。 使用相等篩選器只傳回陣列資料中與指定值相符的專案。

>[!NOTE]
>
>篩選多個欄位時包含`id`或`created`的要求&#x200B;**不**&#x200B;適用於篩選陣列欄位中的多個值。

下列範例查詢只會傳回同時包含`val1`和`val2`的陣列結果。

**API格式**

```http
GET /{OBJECT_TYPE}?property=arrayField=val1&property=arrayField=val2
```

### 不等式篩選器 {#inequality-filters}

在陣列欄位上使用不等式運運算元(`!=`)，以排除資料中陣列包含指定值的任何專案。

**API格式**

```http
GET /{OBJECT_TYPE}?property=arrayField!=val1&property=arrayField!=val2
```

此查詢傳回arrayField不包含`val1`或`val2`的檔案。

### 等式和不等式篩選器限制 {#equality-inequality-limitations}

您無法在單一查詢中將等式(`=`)和不等式(`!=`)同時套用至相同的欄位。
