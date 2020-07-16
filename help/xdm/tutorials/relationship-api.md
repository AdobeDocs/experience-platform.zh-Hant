---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用方案註冊表API定義兩個方案之間的關係
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 1%

---


# 使用 [!DNL Schema Registry] API定義兩個結構之間的關係


Adobe Experience Platform的重要部分，在於能夠跨不同通道瞭解客戶之間的關係以及客戶與品牌之間的互動。 在(XDM)結構中定義這 [!DNL Experience Data Model] 些關係，可讓您獲得客戶資料的複雜見解。

本文檔提供了一個教程，用於定義組織使用定義的兩個方案之間的一對一關係 [!DNL Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。

## 快速入門

本教學課程需要對(XDM) [!DNL Experience Data Model] 和進行有效的瞭解 [!DNL XDM System]。 在開始本教學課程之前，請先閱讀下列檔案：

* [Experience Platform中的XDM系統](../home.md): XDM及其在Experience Platform中的實作概觀。
   * [架構構成基礎](../schema/composition.md): 介紹XDM模式的構建塊。
* [!DNL Real-time Customer Profile](../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

在開始本教學課程之前，請先閱讀開 [發人員指南](../api/getting-started.md) ，以取得成功呼叫 [!DNL Schema Registry] API所需的重要資訊。 這包括您 `{TENANT_ID}`的「容器」概念，以及提出要求所需的標題（請特別注意「接受」標題及其可能的值）。

## 定義源和目標方案 {#define-schemas}

預期您已經建立了將在關係中定義的兩個方案。 本教學課程在組織的當前忠誠度方案（在「忠誠度成員」架構中定義）的成員與其最愛的酒店（在「酒店」架構中定義）之間建立關係。

模式關係由源模式 **[!UICONTROL 表示]** ，該源模式具有引用目標模式內另一欄位的 **[!UICONTROL 欄位]**。 在後續步驟中，「[!UICONTROL Loyalty Members]」將是來源結構描述，而「[!UICONTROL Hotels]」將充當目標結構描述。

要定義兩個方案之間的關係，必須首先獲取兩個 `$id` 方案的值。 如果您知道結構的顯示名`title`稱()，則可以通過向 `$id` API中的端點發出GET請求 `/tenant/schemas` 來查找其 [!DNL Schema Registry] 值。

**API格式**

```http
GET /tenant/schemas
```

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>「接受」標 `application/vnd.adobe.xed-id+json` 題只會傳回產生的結構描述的標題、ID和版本。

**回應**

成功的回應會傳回由您的組織定義的結構清單，包括 `name`其 `$id`、 `meta:altId`和 `version`。

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

記錄 `$id` 要定義之間關係的兩個方案的值。 這些值將用於後續步驟。

## 定義兩個方案的參考欄位

在中，關 [!DNL Schema Registry]系描述符的工作方式與SQL表中的外鍵類似： 源模式中的欄位用作對目標模式欄位的引用。 在定義關係時，每個方案必須有一個專用欄位作為對其他方案的引用。

>[!IMPORTANT]
>
>如果要啟用方案以便在中使用， [!DNL Real-time Customer Profile](../../profile/home.md)則目標方案的引用欄位必須是其主 **[!UICONTROL 要標識]**。 本教學課程稍後會詳細說明此問題。

如果任一方案沒有用於此目的的欄位，您可能需要使用新欄位建立混音，並將其新增至方案。 此新欄位必須 `type` 有&quot;string&quot;值。

在本教學課程中，目標模式&quot;Hotels&quot;已包含一個用於此目的的欄位： `hotelId`. 但是，源模式「忠誠度成員」沒有此欄位，並且必須給予新混音，在其名稱空間下 `favoriteHotel`添加新字 `TENANT_ID` 段。

### 建立新的混音

為了將新欄位添加到方案，必須首先在混合中定義該欄位。 您可以向端點發出POST請求，以建立新混 `/tenant/mixins` 音器。

**API格式**

```http
POST /tenant/mixins
```

**請求**

下列請求會建立新的混音，在所新增 `favoriteHotel` 的任何架構 `TENANT_ID` 的名稱空間下新增欄位。

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**回應**

成功的回應會傳回新建立混合的詳細資料。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| 屬性 | 說明 |
| --- | --- |
| `$id` | 唯讀系統生成新混音的唯一標識符。 以URI的形式。 |

記錄 `$id` mixin的URI，以便在將mixin添加到源模式的下一步驟中使用。

### 將混音添加到源模式

建立混音後，可以通過向端點發出PATCH請求將其添加到源模 `/tenant/schemas/{SCHEMA_ID}` 式。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼的 `$id` URI或 `meta:altId` 來源架構。 |

**請求**

下列請求會將「最愛的酒店」混搭新增至「忠誠會員」結構。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| 屬性 | 說明 |
| --- | --- |
| `op` | 要執行的PATCH操作。 此請求使用操 `add` 作。 |
| `path` | 將添加新資源的模式欄位的路徑。 將混合新增至結構時，值必須為 `/allOf/-`。 |
| `value.$ref` | 要 `$id` 加入的混音。 |

**回應**

成功的響應返回更新模式的詳細資訊，現在該模式在其 `$ref` 陣列下包含添加的混合的 `allOf` 值。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{IMS_ORG}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## 為兩個方案定義主標識欄位

>[!NOTE]
>
>只有在中啟用的方案才需要此步驟 [!DNL Real-time Customer Profile](../../profile/home.md)。 如果不希望任一方案參與聯合，或者如果方案已定義主要標識，則可以跳至為目標方案建立引用標識描述符 [的下一步](#create-descriptor) 。

要在中啟用方案，必須定 [!DNL Real-time Customer Profile]義主標識。 此外，關係的目標模式必須使用其主要標識作為其引用欄位。

在本教程中，源模式已定義了主標識，但目標模式沒有。 通過建立標識描述符，可以將模式欄位標籤為主標識欄位。 這是通過向端點發出POST請求來完 `/tenant/descriptors` 成的。

**API格式**

```http
POST /tenant/descriptors
```

**請求**

以下請求將建立新的身份描述符，該描述符將目 `hotelId` 標方案「Hotels」的欄位定義為主要身份欄位。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| 參數 | 說明 |
| --- | --- |
| `@type` | 要建立的描述符的類型。 身份 `@type` 描述符的值是 `xdm:descriptorIdentity`。 |
| `xdm:sourceSchema` | 在上 `$id` 一步驟中獲取的目標方 [案值](#define-schemas)。 |
| `xdm:sourceVersion` | 方案的版本號。 |
| `sourceProperty` | 將用作方案主要標識的特定欄位的路徑。 此路徑應以&quot;/&quot;開頭，而非以&quot;/&quot;結尾，同時也排除任何&quot;properties&quot;名稱空間。 例如，上述請求會使 `/_{TENANT_ID}/hotelId` 用而非 `/properties/_{TENANT_ID}/properties/hotelId`。 |
| `xdm:namespace` | 身份欄位的身份名稱空間。 `hotelId` 是此範例中的ECID值，因此會使用&quot;ECID&quot;命名空間。 如需可用 [名稱空間的清單](../../identity-service/home.md) ，請參閱身分名稱空間概觀。 |
| `xdm:isPrimary` | 確定標識欄位是否是方案的主標識的布爾屬性。 由於此請求定義了主要身份，因此值設定為true。 |

**回應**

成功的響應返回新建立的身份描述符的詳細資訊。

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## 建立引用標識描述符

如果方案欄位用作關係中其他方案的引用，則必須將引用標識描述符應用到它們。 由於「 `favoriteHotel` 忠誠會員」中的欄位會參照「酒店」中 `hotelId` 的欄位，因此 `hotelId` 必須提供參考身分描述符。

通過向端點發出POST請求，為目標方案建立引用描述 `/tenant/descriptors` 符。

**API格式**

```http
POST /tenant/descriptors
```

**請求**

以下請求為目標方案&quot;Hotels&quot; `hotelId` 中的欄位建立引用描述符。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID"
  }'
```

| 參數 | 說明 |
| --- | --- |
| `xdm:sourceSchema` | 目 `$id` 標架構的URL。 |
| `xdm:sourceVersion` | 目標方案的版本號。 |
| `sourceProperty` | 目標方案的主標識欄位的路徑。 |
| `xdm:identityNamespace` | 參考欄位的身分名稱空間。 `hotelId` 是此範例中的ECID值，因此會使用&quot;ECID&quot;命名空間。 如需可用 [名稱空間的清單](../../identity-service/home.md) ，請參閱身分名稱空間概觀。 |

**回應**

成功的響應返回新建立的目標模式參考描述符的詳細資訊。

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 建立關係描述符 {#create-descriptor}

關係描述符建立源模式和目標模式之間的一對一關係。 通過向端點發出POST請求，可以建立新的關係描述 `/tenant/descriptors` 符。

**API格式**

```http
POST /tenant/descriptors
```

**請求**

以下請求將建立新的關係描述符，其中「忠誠成員」作為源方案，「舊有忠誠成員」作為目標方案。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| 參數 | 說明 |
| --- | --- |
| `@type` | 要建立的描述符的類型。 關係 `@type` 描述符的值是 `xdm:descriptorOneToOne`。 |
| `xdm:sourceSchema` | 源 `$id` 架構的URL。 |
| `xdm:sourceVersion` | 源架構的版本號。 |
| `sourceProperty`: | 源模式中參考欄位的路徑。 |
| `xdm:destinationSchema` | 目 `$id` 標架構的URL。 |
| `xdm:destinationVersion` | 目標方案的版本號。 |
| `destinationProperty`: | 目標方案中參考欄位的路徑。 |

### 回應

成功的響應返回新建立的關係描述符的詳細資訊。

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## 後續步驟

遵循本教學課程，您已成功建立兩個結構之間的一對一關係。 有關使用API描述符的詳細資訊，請參 [!DNL Schema Registry] 閱方案註冊 [開發人員指南](../api/getting-started.md)。 有關如何在UI中定義架構關係的步驟，請參見使用架構編輯器 [定義架構關係的教程](relationship-ui.md)。