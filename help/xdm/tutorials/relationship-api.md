---
keywords: Experience Platform;home；熱門主題；API;XDM;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；模式註冊；模式；模式；模式；模式；關係；關係描述符；關係描述符；參考標識；參考標識；
solution: Experience Platform
title: 使用方案註冊表API定義兩個方案之間的關係
description: 本文檔提供了一個教程，用於定義由組織使用方案註冊表API定義的兩個方案之間的一對一關係。
topic-legacy: tutorial
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 1%

---

# 使用[!DNL Schema Registry] API定義兩個結構之間的關係

瞭解客戶之間的關係以及客戶與品牌之間跨不同通道的互動是Adobe Experience Platform的重要組成部分。 在[!DNL Experience Data Model](XDM)結構中定義這些關係可讓您獲得客戶資料的複雜見解。

雖然架構關係可以通過使用union架構和[!DNL Real-time Customer Profile]來推斷，但這僅適用於共用相同類的架構。 要在屬於不同類的兩個方案之間建立關係，必須將專用的關係欄位添加到源方案中，該源方案引用目標方案的標識。

本文檔提供了一個教程，用於定義組織使用[[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)定義的兩個方案之間的一對一關係。

## 快速入門

本教學課程需要對[!DNL Experience Data Model](XDM)和[!DNL XDM System]有正確的理解。 在開始本教學課程之前，請先閱讀下列檔案：

* [Experience Platform中的XDM系統](../home.md):XDM及其實施概述於 [!DNL Experience Platform]。
   * [架構構成基礎](../schema/composition.md):介紹XDM模式的構建塊。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

在開始本教學課程之前，請先閱讀[開發人員指南](../api/getting-started.md)，以取得成功呼叫[!DNL Schema Registry] API所需的重要資訊。 這包括您的`{TENANT_ID}`、&quot;containers&quot;的概念，以及提出請求的必要標題（請特別注意[!DNL Accept]標題及其可能的值）。

## 定義源和目標方案{#define-schemas}

預期您已經建立了將在關係中定義的兩個方案。 本教學課程在組織的當前忠誠度方案（定義於&quot;[!DNL Loyalty Members]&quot;結構）的成員與其最愛的酒店（定義於&quot;[!DNL Hotels]&quot;結構）之間建立關係。

方案關係由&#x200B;**源方案**&#x200B;表示，該源方案具有引用&#x200B;**目標方案**&#x200B;內另一欄位的欄位。 在後續步驟中，&quot;[!DNL Loyalty Members]&quot;將作為源模式，而&quot;[!DNL Hotels]&quot;將作為目標模式。

>[!IMPORTANT]
>
>為建立關係，兩個方案都必須已定義主要身份，並且必須為[!DNL Real-time Customer Profile]啟用。 如果需要有關如何相應配置方案的指導，請參見架構建立教程中關於[啟用方案以用於Profile](./create-schema-api.md#profile)的章節。

要定義兩個方案之間的關係，必須首先獲取兩個方案的`$id`值。 如果您知道結構的顯示名稱(`title`)，則可以通過向[!DNL Schema Registry] API中的`/tenant/schemas`端點發出GET請求來查找其`$id`值。

**API格式**

```http
GET /tenant/schemas
```

**要求**

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
>[!DNL Accept]標題`application/vnd.adobe.xed-id+json`僅返回結果方案的標題、ID和版本。

**回應**

成功的響應返回由組織定義的方案清單，包括其`name`、`$id`、`meta:altId`和`version`。

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

記錄要定義兩者之間關係的兩個方案的`$id`值。 這些值將用於後續步驟。

## 為源方案定義參考欄位

在[!DNL Schema Registry]中，關係描述符的工作方式與關係資料庫表中的外鍵類似：源模式中的欄位用作對目標模式的主標識欄位的引用。 如果源模式沒有用於此目的的欄位，則可能需要使用新欄位建立模式欄位組並將其添加到模式。 此新欄位必須具有`type`值&quot;[!DNL string]&quot;。

>[!IMPORTANT]
>
>與目標模式不同，源模式不能將其主標識用作參考欄位。

在本教程中，目標方案&quot;[!DNL Hotels]&quot;包含一個`hotelId`欄位，該欄位用作方案的主要標識，因此也將用作其引用欄位。 但是，源模式&quot;[!DNL Loyalty Members]&quot;沒有專用欄位可用作參考，並且必須給出新欄位組，以向模式添加新欄位：`favoriteHotel`。

>[!NOTE]
>
>如果源方案已有您打算用作參考欄位的專用欄位，則可跳至[建立參考描述符](#reference-identity)的步驟。

### 建立新欄位群組

要向方案添加新欄位，必須首先在欄位組中定義該欄位。 您可以通過向`/tenant/fieldgroups`端點發出POST請求來建立新欄位組。

**API格式**

```http
POST /tenant/fieldgroups
```

**要求**

以下請求將建立一個新欄位組，在`_{TENANT_ID}`名稱空間下添加`favoriteHotel`欄位，該名稱空間是所添加到的任何方案。

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
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

成功的回應會傳回新建立欄位群組的詳細資料。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.fieldgroups.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "fieldgroups",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel field group for the Loyalty Members schema.",
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
| `$id` | 唯讀系統生成新欄位組的唯一標識符。 以URI的形式。 |

記錄欄位組的`$id` URI，以便用於將欄位組添加到源模式的下一步。

### 將欄位組添加到源方案

建立欄位組後，可通過向`/tenant/schemas/{SCHEMA_ID}`端點發出PATCH請求將其添加到源模式。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 源架構的URL編碼`$id` URI或`meta:altId`。 |

**要求**

以下請求將&quot;[!DNL Favorite Hotel]&quot;欄位組添加到&quot;[!DNL Loyalty Members]&quot;模式。

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
        "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| 屬性 | 說明 |
| --- | --- |
| `op` | 要執行的PATCH操作。 此請求使用`add`操作。 |
| `path` | 將添加新資源的模式欄位的路徑。 將欄位組添加到方案時，值必須是&quot;/allOf/-&quot;。 |
| `value.$ref` | 要添加的欄位組的`$id`。 |

**回應**

成功的響應返回更新模式的詳細資訊，該模式現在在其`allOf`陣列下包含添加欄位組的`$ref`值。

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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/3387945212ad76ee59b6d2b964afb220"
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
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/61969bc646b66a6230a7e8840f4a4d33"
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

## 建立引用標識描述符{#reference-identity}

如果方案欄位用作關係中其他方案的引用，則必須將引用標識描述符應用到它們。 由於&quot;[!DNL Loyalty Members]&quot;中的`favoriteHotel`欄位將引用&quot;[!DNL Hotels]&quot;中的`hotelId`欄位，因此`hotelId`必須提供參考身份描述符。

通過向`/tenant/descriptors`端點發出POST請求，為目標方案建立引用描述符。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求為目標方案&quot;[!DNL Hotels]&quot;中的`hotelId`欄位建立引用描述符。

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
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| 參數 | 說明 |
| --- | --- |
| `@type` | 正在定義的描述符類型。 對於引用描述符，值必須是&quot;xdm:descriptorReferenceIdentity&quot;。 |
| `xdm:sourceSchema` | 目標架構的`$id` URL。 |
| `xdm:sourceVersion` | 目標方案的版本號。 |
| `sourceProperty` | 目標方案的主標識欄位的路徑。 |
| `xdm:identityNamespace` | 參考欄位的身分名稱空間。 此名稱空間必須與定義欄位作為方案的主標識時使用的名稱空間相同。 如需詳細資訊，請參閱[identity namespace綜覽](../../identity-service/home.md)。 |

**回應**

成功的響應返回新建立的目標模式參考描述符的詳細資訊。

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 建立關係描述符{#create-descriptor}

關係描述符建立源模式和目標模式之間的一對一關係。 在為目標方案定義了引用描述符後，可以通過向`/tenant/descriptors`端點發出POST請求來建立新的關係描述符。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求建立新的關係描述符，其中&quot;[!DNL Loyalty Members]&quot;作為源模式，&quot;[!DNL Legacy Loyalty Members]&quot;作為目標模式。

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
| `@type` | 要建立的描述符的類型。 關係描述符的`@type`值為&quot;xdm:descriptorOneToOne&quot;。 |
| `xdm:sourceSchema` | 源架構的`$id` URL。 |
| `xdm:sourceVersion` | 源架構的版本號。 |
| `xdm:sourceProperty` | 源方案中參考欄位的路徑。 |
| `xdm:destinationSchema` | 目標架構的`$id` URL。 |
| `xdm:destinationVersion` | 目標方案的版本號。 |
| `xdm:destinationProperty` | 目標方案中參考欄位的路徑。 |

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

遵循本教學課程，您已成功建立兩個結構之間的一對一關係。 有關使用[!DNL Schema Registry] API描述符的詳細資訊，請參閱[方案註冊表開發人員指南](../api/descriptors.md)。 有關如何在UI中定義架構關係的步驟，請參見有關使用架構編輯器](relationship-ui.md)定義架構關係的教程。[
