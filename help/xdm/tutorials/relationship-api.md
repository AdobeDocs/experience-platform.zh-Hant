---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構註冊表；結構註冊表；結構；結構；結構；結構；關係；關係描述元；關係描述元；關係描述元；參考身分；參考身分；
title: 使用結構註冊表API定義兩個結構之間的關係
description: 本檔案提供教學課程，說明如何使用Schema Registry API，定義貴組織所定義的兩個結構之間的一對一關係。
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 2%

---

# 使用 [!DNL Schema Registry] API

了解客戶之間的關係，以及客戶在不同管道與品牌互動的能力，是Adobe Experience Platform的重要一環。 在 [!DNL Experience Data Model] (XDM)結構可讓您對客戶資料獲得複雜的深入分析。

而架構關係則可透過使用聯合架構和 [!DNL Real-Time Customer Profile]，此欄位僅適用於共用相同類別的結構。 要在屬於不同類的兩個架構之間建立關係，必須將專用的關係欄位添加到 **來源綱要**，指出個別 **參考綱要**.

>[!NOTE]
>
>Schema Registry API將參考結構稱為「目的地結構」。 這些不得與 [資料準備映射集](../../data-prep/mapping-set.md) 或結構 [目的地連線](../../destinations/home.md).

本檔案提供一個教學課程，用於定義貴組織所定義的兩個結構之間的一對一關係，使用 [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## 快速入門

本教學課程需要深入了解 [!DNL Experience Data Model] (XDM)和 [!DNL XDM System]. 開始本教學課程之前，請檢閱下列檔案：

* [XDM系統Experience Platform](../home.md):XDM及其實作概述 [!DNL Experience Platform].
   * [結構構成基本概念](../schema/composition.md):介紹XDM結構的建置組塊。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

開始本教學課程之前，請檢閱 [開發人員指南](../api/getting-started.md) 以取得您需要知道的重要資訊，以便成功對 [!DNL Schema Registry] API。 這包括 `{TENANT_ID}`、「容器」的概念，以及提出要求所需的標題(請特別注意 [!DNL Accept] 標題及其可能的值)。

## 定義源和引用架構 {#define-schemas}

您應已建立將在關係中定義的兩個結構。 本教學課程會建立組織目前忠誠計畫成員(定義於「[!DNL Loyalty Members]」和其最喜愛的酒店(定義於「[!DNL Hotels]&quot;架構)。

架構關係由 **來源綱要** 在 **參考綱要**. 在下列步驟中，「[!DNL Loyalty Members]&quot;將是源架構，而&quot;[!DNL Hotels]「 」將作為參考架構。

>[!IMPORTANT]
>
>若要建立關係，兩個結構都必須定義主要身分，並啟用 [!DNL Real-Time Customer Profile]. 請參閱 [啟用結構以用於配置檔案](./create-schema-api.md#profile) 如果您需要如何據以設定結構的指引，請參閱結構建立教學課程。

若要定義兩個結構之間的關係，您必須先取得 `$id` 值。 如果您知道顯示名稱(`title`)，您可以找到其 `$id` 值，方法是向 `/tenant/schemas` 端點 [!DNL Schema Registry] API。

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
>此 [!DNL Accept] 標題 `application/vnd.adobe.xed-id+json` 僅傳回產生結構的標題、ID和版本。

**回應**

成功的回應會傳回貴組織定義的結構清單，包括其 `name`, `$id`, `meta:altId`，和 `version`.

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

記錄 `$id` 要定義之間關係的兩個結構的值。 這些值將用於後續步驟。

## 為源架構定義引用欄位

在 [!DNL Schema Registry]，關係描述符與關係資料庫表中的外鍵類似：源架構中的欄位用作參考架構的主要標識欄位的參考。 如果源架構沒有用於此目的的欄位，則可能需要使用新欄位建立架構欄位組，並將其添加到架構中。 此新欄位必須具有 `type` 值 `string`.

>[!IMPORTANT]
>
>源架構不能將其主標識用作引用欄位。

在本教學課程中，參考結構「[!DNL Hotels]&quot;包含 `hotelId` 作為結構主要身分的欄位。 但源架構「[!DNL Loyalty Members]&quot;沒有專用欄位可用作的引用 `hotelId`，因此需要建立自訂欄位群組，才能將新欄位新增至結構： `favoriteHotel`.

>[!NOTE]
>
>如果源架構已有您計畫用作參考欄位的專用欄位，則可以跳到上的步驟 [建立引用描述符](#reference-identity).

### 建立新欄位群組

若要將新欄位新增至結構，必須先在欄位群組中定義欄位。 您可以向 `/tenant/fieldgroups` 端點。

**API格式**

```http
POST /tenant/fieldgroups
```

**要求**

下列請求會建立新欄位群組，以新增 `favoriteHotel` 欄位 `_{TENANT_ID}` 其新增至的任何架構的命名空間。

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

成功的回應會傳回新建立欄位群組的詳細資訊。

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
| `$id` | 只讀，系統生成新欄位組的唯一標識符。 以URI的形式。 |

{style=&quot;table-layout:auto&quot;}

記錄 `$id` 欄位組的URI，用於將欄位組添加到源架構的下一步。

### 將欄位組添加到源架構

建立欄位群組後，您可以向 `/tenant/schemas/{SCHEMA_ID}` 端點。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 源架構的。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會新增「[!DNL Favorite Hotel]&quot;欄位組到&quot;[!DNL Loyalty Members]」架構。

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
| `op` | 要執行的PATCH操作。 此請求使用 `add` 操作。 |
| `path` | 新增新資源的架構欄位路徑。 將欄位群組新增至結構時，值必須是「/allOf/ — 」。 |
| `value.$ref` | 此 `$id` 的欄位組。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回更新架構的詳細資訊，現在包含 `$ref` 新增欄位群組在其下的值 `allOf` 陣列。

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

## 建立引用標識描述符 {#reference-identity}

如果架構欄位被用作關係中其他架構的引用，則它們必須應用引用標識描述符。 由於 `favoriteHotel` 欄位[!DNL Loyalty Members]「 」將指 `hotelId` 欄位[!DNL Hotels]&quot;, `favoriteHotel` 必須給定引用標識描述符。

通過向發送POST請求，為源架構建立引用描述符 `/tenant/descriptors` 端點。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求將為 `favoriteHotel` 欄位(在源架構「[!DNL Loyalty Members]」。

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
| `@type` | 要定義的描述符的類型。 對於引用描述符，值必須是 `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | 此 `$id` 源架構的URL。 |
| `xdm:sourceVersion` | 源架構的版本號。 |
| `sourceProperty` | 源架構中用於引用引用架構的主要標識的欄位路徑。 |
| `xdm:identityNamespace` | 參考欄位的身分命名空間。 這必須與參考架構的主要身分相同的命名空間。 請參閱 [身分命名空間概述](../../identity-service/home.md) 以取得更多資訊。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的響應返回源欄位新建的引用描述符的詳細資訊。

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

## 建立關係描述符 {#create-descriptor}

關係描述符建立源模式和參考模式之間的一對一關係。 在為源架構中的相應欄位定義了引用標識描述符後，您可以通過向POST請求建立新的關係描述符 `/tenant/descriptors` 端點。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求將建立新的關係描述符，其中「[!DNL Loyalty Members]&quot;作為源架構，而&quot;[!DNL Hotels]」作為參考架構。

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
| `@type` | 要建立的描述符的類型。 此 `@type` 關係描述符的值 `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | 此 `$id` 源架構的URL。 |
| `xdm:sourceVersion` | 源架構的版本號。 |
| `xdm:sourceProperty` | 源架構中引用欄位的路徑。 |
| `xdm:destinationSchema` | 此 `$id` 參考結構的URL。 |
| `xdm:destinationVersion` | 參考架構的版本號。 |
| `xdm:destinationProperty` | 引用架構中主標識欄位的路徑。 |

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

依照本教學課程，您已成功建立兩個結構間的一對一關係。 有關使用描述符的詳細資訊，請使用 [!DNL Schema Registry] API，請參閱 [Schema Registry開發人員指南](../api/descriptors.md). 如需在UI中定義結構關係的步驟，請參閱 [使用架構編輯器定義架構關係](relationship-ui.md).
