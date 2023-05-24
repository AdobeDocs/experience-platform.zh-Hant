---
keywords: Experience Platform；主題；熱門主題；api;XDM;XDM;XDM系統；經驗資料模型；體驗資料模型；資料模型；資料模型；資料模型；架構註冊；架構；架構；架構；架構；關係；關係描述符；關係描述符；參考身份；
title: 使用架構註冊表API定義兩個架構之間的關係
description: 本文檔提供了一個教程，用於定義組織使用架構註冊表API定義的兩個架構之間的一對一關係。
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 1%

---

# 使用 [!DNL Schema Registry] API

瞭解客戶之間的關係以及客戶與品牌之間通過各種渠道進行的互動是Adobe Experience Platform的重要部分。 在結構中定義這些關係 [!DNL Experience Data Model] (XDM)架構使您能夠對客戶資料獲得複雜的見解。

而架構關係可通過使用聯合架構和 [!DNL Real-Time Customer Profile]，這僅適用於共用同一類的方案。 要在屬於不同類的兩個架構之間建立關係，必須將專用關係欄位添加到 **源架構**，表示單獨 **參考模式**。

>[!NOTE]
>
>架構註冊表API將引用架構稱為「目標架構」。 不要將這些與中的目標架構混淆 [資料準備映射集](../../data-prep/mapping-set.md) 或架構 [目標連接](../../destinations/home.md)。

本文檔提供了一個教程，用於定義由您的組織使用 [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。

## 快速入門

本教程要求您對 [!DNL Experience Data Model] (XDM)和 [!DNL XDM System]。 在開始本教程之前，請查看以下文檔：

* [XDM系統在Experience Platform](../home.md):XDM及其在XDM中的應用 [!DNL Experience Platform]。
   * [架構組合的基礎](../schema/composition.md):介紹了XDM模式的構件。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

在開始本教程之前，請複習 [開發者指南](../api/getting-started.md) 獲取您需要瞭解的重要資訊，以便成功撥打 [!DNL Schema Registry] API。 這包括您 `{TENANT_ID}`、&quot;容器&quot;的概念以及提出請求所需的標題(特別注意 [!DNL Accept] 標題及其可能值)。

## 定義源和引用方案 {#define-schemas}

預期您已經建立了將在關係中定義的兩個架構。 本教程在組織的當前會員計畫（在「」中定義）的成員之間建立關係[!DNL Loyalty Members]&quot;架構及其最喜愛的酒店(在「[!DNL Hotels]&quot;架構)。

架構關係由 **源架構** 有一個欄位，該欄位引用 **參考模式**。 在後續步驟中， &quot;[!DNL Loyalty Members]&quot;將是源架構，而&quot;[!DNL Hotels]&quot;將用作引用架構。

>[!IMPORTANT]
>
>要建立關係，兩個方案必須都定義了主標識並且都為 [!DNL Real-Time Customer Profile]。 請參閱 [啟用在配置檔案中使用的架構](./create-schema-api.md#profile) 在架構建立教程中，如果您需要有關如何相應地配置架構的指導。

要定義兩個方案之間的關係，必須首先獲取 `$id` 兩個方案的值。 如果您知道顯示名稱(`title`)，您可以找到 `$id` 值，方法是向 `/tenant/schemas` 端點 [!DNL Schema Registry] API。

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
>的 [!DNL Accept] 標題 `application/vnd.adobe.xed-id+json` 僅返回結果架構的標題、ID和版本。

**回應**

成功的響應返回由組織定義的方案清單，包括其 `name`。 `$id`。 `meta:altId`, `version`。

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

錄制 `$id` 要定義之間關係的兩個方案的值。 這些值將在後續步驟中使用。

## 定義源方案的引用欄位

在 [!DNL Schema Registry]，關係描述符在關係資料庫表中的工作與外鍵類似：源架構中的欄位用作引用架構的主標識欄位的引用。 如果源架構沒有用於此目的的欄位，則可能需要使用新欄位建立架構欄位組並將其添加到架構中。 此新欄位必須具有 `type` 值 `string`。

>[!IMPORTANT]
>
>源架構不能將其主標識用作引用欄位。

在本教程中，引用架構「」[!DNL Hotels]&quot;包含 `hotelId` 用作架構主標識的欄位。 但是，源架構&quot;[!DNL Loyalty Members]&quot;沒有要用作引用的專用欄位 `hotelId`，因此需要建立自定義欄位組，以便向架構添加新欄位： `favoriteHotel`。

>[!NOTE]
>
>如果源架構已有一個您計畫用作引用欄位的專用欄位，則可以跳到上的步驟 [建立引用描述符](#reference-identity)。

### 建立新欄位組

要向架構添加新欄位，必須先在欄位組中定義該欄位。 您可以通過向 `/tenant/fieldgroups` 端點。

**API格式**

```http
POST /tenant/fieldgroups
```

**要求**

以下請求將建立一個新欄位組， `favoriteHotel` 欄位 `_{TENANT_ID}` 添加到的任何架構的命名空間。

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

成功的響應將返回新建立的欄位組的詳細資訊。

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
| `$id` | 只讀，系統生成了新欄位組的唯一標識符。 以URI的形式。 |

{style="table-layout:auto"}

錄制 `$id` 將欄位組添加到源架構的下一步中使用的欄位組的URI。

### 將欄位組添加到源架構

建立欄位組後，可以通過向PATCH請求將其添加到源架構 `/tenant/schemas/{SCHEMA_ID}` 端點。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 源架構。 |

{style="table-layout:auto"}

**要求**

以下請求將添加「[!DNL Favorite Hotel]&quot;欄位組到&quot;[!DNL Loyalty Members]&quot;架構。

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
| `op` | 要執行的PATCH操作。 此請求使用 `add` 的下界。 |
| `path` | 將添加新資源的架構欄位的路徑。 將欄位組添加到架構時，值必須為「/allOf/ — 」。 |
| `value.$ref` | 的 `$id` 的子菜單。 |

{style="table-layout:auto"}

**回應**

成功的響應返回更新的架構的詳細資訊，現在包括 `$ref` 其下添加的欄位組的值 `allOf` 陣列。

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

如果將架構欄位用作對關係中另一個架構的引用，則它們必須應用引用標識描述符。 自 `favoriteHotel` 欄位「」[!DNL Loyalty Members]」將引用 `hotelId` 欄位「」[!DNL Hotels]&quot; `favoriteHotel` 必須給出引用標識描述符。

通過向源架構發出POST請求，為其建立引用描述符 `/tenant/descriptors` 端點。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求為 `favoriteHotel` 源架構「」中的欄位[!DNL Loyalty Members]。

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
| `@type` | 正在定義的描述符的類型。 對於引用描述符，值必須為 `xdm:descriptorReferenceIdentity`。 |
| `xdm:sourceSchema` | 的 `$id` 源架構的URL。 |
| `xdm:sourceVersion` | 源架構的版本號。 |
| `sourceProperty` | 源架構中用於引用引用架構的主標識的欄位的路徑。 |
| `xdm:identityNamespace` | 引用欄位的標識名稱空間。 這必須與引用架構的主標識相同的命名空間。 查看 [標識命名空間概述](../../identity-service/home.md) 的子菜單。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回新建立的源欄位引用描述符的詳細資訊。

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

關係描述符在源模式和參考模式之間建立一對一關係。 在源架構中為相應欄位定義了引用標識描述符後，可以通過向POST請求建立新的關係描述符 `/tenant/descriptors` 端點。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求將建立新的關係描述符，其中包含「[!DNL Loyalty Members]&quot;作為源架構和&quot;[!DNL Hotels]」作為引用架構。

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
| `@type` | 要建立的描述符的類型。 的 `@type` 關係描述符的值 `xdm:descriptorOneToOne`。 |
| `xdm:sourceSchema` | 的 `$id` 源架構的URL。 |
| `xdm:sourceVersion` | 源架構的版本號。 |
| `xdm:sourceProperty` | 源架構中引用欄位的路徑。 |
| `xdm:destinationSchema` | 的 `$id` 引用架構的URL。 |
| `xdm:destinationVersion` | 引用架構的版本號。 |
| `xdm:destinationProperty` | 引用架構中主標識欄位的路徑。 |

{style="table-layout:auto"}

### 回應

成功的響應將返回新建立的關係描述符的詳細資訊。

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

按照本教程，您已成功在兩個架構之間建立了一對一關係。 有關使用描述符的詳細資訊 [!DNL Schema Registry] API，請參見 [架構註冊表開發人員指南](../api/descriptors.md)。 有關如何在UI中定義架構關係的步驟，請參見上的教程 [使用架構編輯器定義架構關係](relationship-ui.md)。
