---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述；結構描述；結構描述；關係；關係描述項；參考身分；參考身分；
title: 使用結構描述登入API定義兩個結構描述之間的關係
description: 本檔案提供教學課程，說明如何使用Schema Registry API定義由您的組織定義之兩個結構描述間的一對一關係。
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 1%

---

# 使用[!DNL Schema Registry] API定義兩個結構描述之間的關係

瞭解客戶之間的關係以及他們跨不同管道與您品牌的互動，是Adobe Experience Platform的重要一環。 在[!DNL Experience Data Model] (XDM)結構描述的結構中定義這些關係，可讓您獲得有關客戶資料的複雜見解。

雖然結構描述關聯性可透過使用聯合結構描述和[!DNL Real-Time Customer Profile]來推斷，但這僅適用於共用相同類別的結構描述。 若要在屬於不同類別的兩個結構描述之間建立關聯性，必須將專用關聯性欄位新增到&#x200B;**來源結構描述**，以表示個別&#x200B;**參考結構描述**&#x200B;的識別。

>[!NOTE]
>
>結構描述登入API會將參照結構描述稱為「目的地結構描述」。 請勿將這些與[資料準備對應集](../../data-prep/mapping-set.md)中的目的地結構描述或[目的地連線](../../destinations/home.md)的結構描述混淆。

本檔案提供教學課程，用於定義貴組織使用[[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)定義之兩個結構描述間的一對一關係。

## 快速入門

此教學課程需要實際瞭解[!DNL Experience Data Model] (XDM)和[!DNL XDM System]。 在開始本教學課程之前，請先檢閱下列檔案：

* Experience Platform中的[XDM系統](../home.md)： [!DNL Experience Platform]中XDM及其實作的概觀。
   * [結構描述組合的基本概念](../schema/composition.md)： XDM結構描述的建置區塊簡介。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

開始進行此教學課程之前，請檢閱[開發人員指南](../api/getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫[!DNL Schema Registry] API。 這包括您的`{TENANT_ID}`、「容器」的概念以及發出要求所需的標頭（特別注意[!DNL Accept]標頭及其可能的值）。

## 定義來源和參考結構描述 {#define-schemas}

您應已建立將在關係中定義的兩個結構描述。 此教學課程會建立組織目前熟客方案（定義在「[!DNL Loyalty Members]」結構描述中）的成員與其最愛的飯店（定義在「[!DNL Hotels]」結構描述中）之間的關係。

結構描述關係由&#x200B;**來源結構描述**&#x200B;表示，該結構描述具有參照&#x200B;**參考結構描述**&#x200B;內其他欄位的欄位。 在接下來的步驟中，&quot;[!DNL Loyalty Members]&quot;將會是來源結構描述，而&quot;[!DNL Hotels]&quot;將會做為參考結構描述。

>[!IMPORTANT]
>
>為了建立關聯性，兩個結構描述都必須定義主要身分並啟用[!DNL Real-Time Customer Profile]。 如果您需要如何適當地設定結構描述的指引，請參閱結構描述建立教學課程中[啟用結構描述以用於設定檔](./create-schema-api.md#profile)的區段。

若要定義兩個結構描述之間的關係，您必須先取得兩個結構描述的`$id`值。 如果您知道結構描述的顯示名稱(`title`)，您可以對[!DNL Schema Registry] API中的`/tenant/schemas`端點發出GET要求來尋找其`$id`值。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>[!DNL Accept]標題`application/vnd.adobe.xed-id+json`只會傳回產生的結構描述的標題、ID和版本。

**回應**

成功的回應會傳回您組織定義的結構描述清單，包括其`name`、`$id`、`meta:altId`和`version`。

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

記錄您要定義關聯性的兩個結構描述的`$id`值。 這些值將在後續步驟中使用。

## 定義來源結構描述的參考欄位

在[!DNL Schema Registry]中，關聯描述項的工作方式與關聯式資料庫表格中的外來索引鍵類似：來源結構描述中的欄位會作為參考結構描述之主要身分欄位的參考。 如果您的來源結構描述沒有用於此目的的欄位，您可能需要使用新欄位建立結構描述欄位群組，並將其新增到結構描述。 此新欄位必須有`type`值`string`。

>[!IMPORTANT]
>
>來源結構描述不能使用其主要身分作為參考欄位。

在本教學課程中，參考結構描述&quot;[!DNL Hotels]&quot;包含作為結構描述主要身分的`hotelId`欄位。 然而，來源結構描述&quot;[!DNL Loyalty Members]&quot;沒有專用欄位可作為`hotelId`的參考，因此需要建立自訂欄位群組，才能將新欄位新增至結構描述： `favoriteHotel`。

>[!NOTE]
>
>如果您的來源結構描述已有您打算用作參考欄位的專用欄位，您可以直接跳到[建立參考描述項](#reference-identity)的步驟。

### 建立新的欄位群組

為了將新欄位新增到結構描述，必須首先在欄位群組中定義它。 您可以對`/tenant/fieldgroups`端點發出POST要求，以建立新的欄位群組。

**API格式**

```http
POST /tenant/fieldgroups
```

**要求**

以下請求會建立新的欄位群組，該群組會在其加入的任何結構描述的`_{TENANT_ID}`名稱空間下新增`favoriteHotel`欄位。

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的回應會傳回新建立的欄位群組的詳細資料。

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
| `$id` | 新欄位群組的唯讀、系統產生的唯一識別碼。 採用URI的形式。 |

{style="table-layout:auto"}

記錄欄位群組的`$id` URI，以用於下一步將欄位群組新增至來源結構描述中。

### 將欄位群組新增至來源結構描述

建立欄位群組後，您可以對`/tenant/schemas/{SCHEMA_ID}`端點發出PATCH請求，將其新增至來源結構描述。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | 來源結構描述的URL編碼`$id` URI或`meta:altId`。 |

{style="table-layout:auto"}

**要求**

下列請求將&quot;[!DNL Favorite Hotel]&quot;欄位群組新增至&quot;[!DNL Loyalty Members]&quot;結構描述。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | 要執行的PATCH操作。 此要求使用`add`作業。 |
| `path` | 要新增新資源的結構描述欄位的路徑。 將欄位群組新增到結構描述時，值必須是&quot;/allOf/-&quot;。 |
| `value.$ref` | 要新增的欄位群組的`$id`。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回更新結構描述的詳細資料，現在包含新增欄位群組在其`allOf`陣列下的`$ref`值。

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
    "imsOrg": "{ORG_ID}",
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

## 建立參考身分描述項 {#reference-identity}

如果結構描述欄位用作關係中另一個結構描述的參考，則這些結構描述欄位必須套用參考身分描述項。 由於「[!DNL Loyalty Members]」中的`favoriteHotel`欄位將參考「[!DNL Hotels]」中的`hotelId`欄位，因此`favoriteHotel`必須被指定參考身分描述項。

藉由對`/tenant/descriptors`端點發出POST要求，建立來源結構描述的參考描述項。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

下列要求會在來源結構描述&quot;[!DNL Loyalty Members]&quot;中建立`favoriteHotel`欄位的參考描述項。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| 參數 | 說明 |
| --- | --- |
| `@type` | 正在定義的描述項型別。 參考描述項的值必須是`xdm:descriptorReferenceIdentity`。 |
| `xdm:sourceSchema` | 來源結構描述的`$id` URL。 |
| `xdm:sourceVersion` | 來源結構描述的版本號碼。 |
| `sourceProperty` | 來源結構描述中用於參考參考結構描述主要身分的欄位路徑。 |
| `xdm:identityNamespace` | 參考欄位的身分名稱空間。 此名稱空間必須與參考結構描述的主要身分相同。 如需詳細資訊，請參閱[身分名稱空間概觀](../../identity-service/home.md)。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回來源欄位新建立的參考描述項的詳細資料。

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 建立關係描述項 {#create-descriptor}

關係描述元在來源結構描述和參考結構描述之間建立一對一的關係。 一旦您在來源結構描述中定義了適當欄位的參考身分描述項，您就可以對`/tenant/descriptors`端點發出POST要求，以建立新的關係描述項。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求會建立新的關係描述項，並將&quot;[!DNL Loyalty Members]&quot;當作來源結構描述，並將&quot;[!DNL Hotels]&quot;當作參考結構描述。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `@type` | 要建立的描述項型別。 關聯性描述項的`@type`值為`xdm:descriptorOneToOne`。 |
| `xdm:sourceSchema` | 來源結構描述的`$id` URL。 |
| `xdm:sourceVersion` | 來源結構描述的版本號碼。 |
| `xdm:sourceProperty` | 來源結構描述中參考欄位的路徑。 |
| `xdm:destinationSchema` | 參考結構描述的`$id` URL。 |
| `xdm:destinationVersion` | 參考結構描述的版本號碼。 |
| `xdm:destinationProperty` | 參照結構描述中主要身分欄位的路徑。 |

{style="table-layout:auto"}

### 回應

成功的回應會傳回新建立的關係描述項的詳細資料。

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

依照本教學課程，您已成功建立兩個結構描述之間的一對一關係。 如需使用[!DNL Schema Registry] API使用描述元的詳細資訊，請參閱[結構描述登入開發人員指南](../api/descriptors.md)。 如需有關如何在UI中定義結構描述關係的步驟，請參閱有關[使用結構描述編輯器定義結構描述關係的教學課程](relationship-ui.md)。
