---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構註冊表；結構註冊表；結構；結構；結構；結構；關係；關係描述元；關係描述元；關係描述元；參考身分；參考身分；
solution: Experience Platform
title: 使用結構註冊表API定義兩個結構之間的關係
description: 本檔案提供教學課程，說明如何使用Schema Registry API，定義貴組織所定義的兩個結構之間的一對一關係。
topic-legacy: tutorial
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 2%

---

# 使用[!DNL Schema Registry] API定義兩個結構之間的關係

了解客戶之間的關係，以及客戶在不同管道與品牌互動的能力，是Adobe Experience Platform的重要一環。 在[!DNL Experience Data Model](XDM)結構內定義這些關係，可讓您對客戶資料獲得複雜的深入分析。

雖然可透過使用聯合架構和[!DNL Real-time Customer Profile]來推斷架構關係，但這隻適用於共用相同類別的架構。 要在屬於不同類的兩個架構之間建立關係，必須將專用的關係欄位添加到源架構中，該源架構引用目標架構的標識。

本檔案提供教學課程，說明如何使用[[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)來定義貴組織所定義的兩個結構之間的一對一關係。

## 快速入門

本教學課程需要妥善了解[!DNL Experience Data Model](XDM)和[!DNL XDM System]。 開始本教學課程之前，請檢閱下列檔案：

* [Experience Platform中的XDM系統](../home.md):概略說明XDM及其實作方 [!DNL Experience Platform]式。
   * [結構構成基本概念](../schema/composition.md):介紹XDM結構的建置組塊。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

開始本教學課程之前，請檢閱[開發人員指南](../api/getting-started.md)，以取得您需要了解的重要資訊，以便成功呼叫[!DNL Schema Registry] API。 這包括您的`{TENANT_ID}`、「容器」的概念，以及提出請求所需的標題（請特別注意[!DNL Accept]標題及其可能的值）。

## 定義源和目標架構{#define-schemas}

您應已建立將在關係中定義的兩個結構。 本教學課程會在組織的目前忠誠計畫（在「[!DNL Loyalty Members]」架構中定義）的成員與其最喜愛的酒店（在「[!DNL Hotels]」架構中定義）之間建立關係。

架構關係由&#x200B;**源架構**&#x200B;表示，該源架構具有引用&#x200B;**目標架構**&#x200B;內另一欄位的欄位。 在後續步驟中，「[!DNL Loyalty Members]」將是源架構，而「[!DNL Hotels]」將充當目標架構。

>[!IMPORTANT]
>
>若要建立關係，兩個結構都必須定義主要身分，並且必須為[!DNL Real-time Customer Profile]啟用。 如果您需要如何據以設定結構的指引，請參閱架構建立教學課程中[啟用結構以用於Profile](./create-schema-api.md#profile)的一節。

若要定義兩個結構之間的關係，您必須先取得兩個結構的`$id`值。 如果您知道結構的顯示名稱(`title`)，則可以在[!DNL Schema Registry] API中向`/tenant/schemas`端點提出GET要求，以找到其`$id`值。

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
>[!DNL Accept]標題`application/vnd.adobe.xed-id+json`僅傳回結果結構的標題、ID和版本。

**回應**

成功的回應會傳回您的組織所定義的結構清單，包括其`name`、`$id`、`meta:altId`和`version`。

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

記錄要定義兩者間關係的`$id`值。 這些值將用於後續步驟。

## 為源架構定義引用欄位

在[!DNL Schema Registry]中，關係描述符的工作方式與關係資料庫表中的外鍵類似：源架構中的欄位用作目標架構的主標識欄位的引用。 如果源架構沒有用於此目的的欄位，則可能需要使用新欄位建立架構欄位組，並將其添加到架構中。 此新欄位的`type`值必須為「[!DNL string]」。

>[!IMPORTANT]
>
>與目標架構不同，源架構不能將其主標識用作引用欄位。

在本教程中，目標架構「[!DNL Hotels]」包含`hotelId`欄位，該欄位用作架構的主要標識，因此也將用作其引用欄位。 但是，源架構「[!DNL Loyalty Members]」沒有專用欄位可用作引用，必須為其指定一個新欄位組，以向架構添加新欄位：`favoriteHotel`。

>[!NOTE]
>
>如果源架構已有您計畫用作參考欄位的專用欄位，則可跳到[建立參考描述符](#reference-identity)上的步驟。

### 建立新欄位群組

若要將新欄位新增至結構，必須先在欄位群組中定義欄位。 您可以向`/tenant/fieldgroups`端點提出POST請求，以建立新欄位組。

**API格式**

```http
POST /tenant/fieldgroups
```

**要求**

下列請求會建立新欄位群組，在其新增至之任何架構的`_{TENANT_ID}`命名空間下新增`favoriteHotel`欄位。

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

成功的回應會傳回新建立欄位群組的詳細資訊。

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
| `$id` | 只讀，系統生成新欄位組的唯一標識符。 以URI的形式。 |

{style=&quot;table-layout:auto&quot;}

記錄欄位組的`$id` URI，以用於將欄位組添加到源架構的下一步。

### 將欄位組添加到源架構

建立欄位組後，可以通過向`/tenant/schemas/{SCHEMA_ID}`端點發出PATCH請求將其添加到源架構。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 源架構的URL編碼的`$id` URI或`meta:altId`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求將「[!DNL Favorite Hotel]」欄位組添加到「[!DNL Loyalty Members]」架構中。

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
| `path` | 新增新資源的架構欄位路徑。 將欄位群組新增至結構時，值必須是「/allOf/ — 」。 |
| `value.$ref` | 要添加的欄位組的`$id`。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回更新架構的詳細資訊，現在包含新增欄位群組`allOf`陣列下的`$ref`值。

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

如果方案欄位用作關係中其他方案的引用，則必須將引用標識描述符應用到它們。 由於「[!DNL Loyalty Members]」中的`favoriteHotel`欄位將引用「[!DNL Hotels]」中的`hotelId`欄位，因此`hotelId`必須獲得引用標識描述符。

通過向`/tenant/descriptors`端點發出POST請求，為目標架構建立引用描述符。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求為目標架構「[!DNL Hotels]」中的`hotelId`欄位建立引用描述符。

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
| `@type` | 要定義的描述符的類型。 對於引用描述符，值必須是&quot;xdm:descriptorReferenceIdentity&quot;。 |
| `xdm:sourceSchema` | 目標架構的`$id` URL。 |
| `xdm:sourceVersion` | 目標架構的版本號。 |
| `sourceProperty` | 目標架構的主要身份欄位的路徑。 |
| `xdm:identityNamespace` | 參考欄位的身分命名空間。 這必須與將欄位定義為架構的主要身分時使用的命名空間相同。 如需詳細資訊，請參閱[身分命名空間概述](../../identity-service/home.md) 。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的響應返回目標架構新建的引用描述符的詳細資訊。

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

關係描述符在源模式和目標模式之間建立一對一關係。 為目標架構定義了引用描述符後，可以通過向`/tenant/descriptors`端點發出POST請求來建立新的關係描述符。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求將建立新的關係描述符，其中「[!DNL Loyalty Members]」作為源架構，「[!DNL Legacy Loyalty Members]」作為目標架構。

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
| `xdm:sourceProperty` | 源架構中引用欄位的路徑。 |
| `xdm:destinationSchema` | 目標架構的`$id` URL。 |
| `xdm:destinationVersion` | 目標架構的版本號。 |
| `xdm:destinationProperty` | 目標架構中引用欄位的路徑。 |

{style=&quot;table-layout:auto&quot;}

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

依照本教學課程，您已成功建立兩個結構間的一對一關係。 有關使用[!DNL Schema Registry] API的描述符的詳細資訊，請參閱[Schema Registry開發者指南](../api/descriptors.md)。 有關如何在UI中定義架構關係的步驟，請參閱有關使用架構編輯器](relationship-ui.md)定義架構關係的教程。[
