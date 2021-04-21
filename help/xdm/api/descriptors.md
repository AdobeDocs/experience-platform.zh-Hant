---
keywords: Experience Platform;home；熱門主題；api;XDM;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；模式註冊；描述符；描述符；描述符；標識；身份；友好名稱；友好名稱；替代顯示資訊；參考；關係；關係
solution: Experience Platform
title: 描述符API端點
description: 方案註冊表API中的／描述符端點允許您在體驗應用程式中以寫程式方式管理XDM描述符。
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1611'
ht-degree: 1%

---

# 描述符端點

結構定義資料實體的靜態視圖，但不提供基於這些結構的資料（例如資料集）如何彼此關聯的具體詳細資訊。 Adobe Experience Platform允許您使用描述符描述這些關係和關於模式的其他解釋性元資料。

架構描述子是租用戶層級的中繼資料，這表示它們對您的IMS組織是獨一無二的，所有描述子操作都發生在租用戶容器中。

每個模式都可以應用一個或多個模式描述符實體。 每個方案描述符實體都包含一個`@type`描述符和它所應用的`sourceSchema`。 應用後，這些描述符將應用於使用模式建立的所有資料集。

[!DNL Schema Registry] API中的`/descriptors`端點可讓您以程式設計方式管理體驗應用程式中的描述子。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需之必要標題的重要資訊。

## 檢索描述符{#list}的清單

通過向`/tenant/descriptors`發出GET請求，可以列出組織已定義的所有描述符。

**API格式**

```http
GET /tenant/descriptors
```

**要求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

回應格式取決於請求中傳送的`Accept`標題。 請注意，`/descriptors`端點使用的`Accept`標題與[!DNL Schema Registry] API中的所有其他端點不同。

>[!IMPORTANT]
>
>描述符需要唯一的`Accept`標頭，用`xdm`替換`xed`，並提供描述符唯一的`link`選項。 下列範例呼叫中已包含正確的`Accept`標題，但請格外小心，以確保使用描述符時使用正確的標題。

| `Accept` 標題 | 說明 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID的陣列 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路徑的陣列 |
| `application/vnd.adobe.xdm+json` | 返回擴展描述符對象的陣列 |
| `application/vnd.adobe.xdm-v2+json` | 必須使用此`Accept`標頭才能使用分頁功能。 |

**回應**

該響應包括用於具有已定義描述符的每個描述符類型的陣列。 換言之，如果沒有定義某個`@type`描述符，則註冊表將不會為該描述符類型返回空陣列。

使用`link` `Accept`標題時，每個描述符都顯示為`/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`格式的陣列項

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## 查找描述符{#lookup}

如果要查看特定描述符的詳細資訊，可以使用其`@id`查找(GET)單個描述符。

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要查找的描述符的`@id`。 |

**要求**

以下請求通過`@id`值檢索描述符。 描述符未版本化，因此查找請求中不需要`Accept`標題。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回描述符的詳細資訊，包括其`@type`和`sourceSchema`，以及根據描述符類型而有所不同的其他資訊。 傳回的`@id`應符合請求中提供的描述符`@id`。

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{IMS_ORG}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 建立描述符{#create}

通過向`/tenant/descriptors`端點發出POST請求，可以建立新描述符。

>[!IMPORTANT]
>
>[!DNL Schema Registry]允許您定義幾種不同的描述符類型。 每個描述符類型都需要在請求主體中發送其自己的特定欄位。 有關描述符的完整清單以及定義它們所需的欄位，請參見[附錄](#defining-descriptors)。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求在示例方案的「電子郵件地址」欄位上定義身份描述符。 這會告訴[!DNL Experience Platform]使用電子郵件地址做為識別碼，以協助將個人的相關資訊結合在一起。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**回應**

成功的響應返回HTTP狀態201（已建立）和新建立的描述符的詳細資訊，包括其`@id`。 `@id`是[!DNL Schema Registry]指派的唯讀欄位，用於參照API中的描述符。

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 更新描述符{#put}

通過將描述符`@id`包含在PUT請求的路徑中，可以更新描述符。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要更新的描述符的`@id`。 |

**要求**

此請求實際上重寫描述符，因此請求主體必須包含定義該類型描述符所需的所有欄位。 換言之，用於更新(PUT)描述符的請求裝載與將[裝載建立(POST)同類型的描述符](#create)的裝載相同。

>[!IMPORTANT]
>
>與使用POST請求建立描述符一樣，每個描述符類型都要求在PUT請求負載中發送其自己的特定欄位。 有關描述符的完整清單以及定義它們所需的欄位，請參見[附錄](#defining-descriptors)。

下面的示例更新身份描述符以引用不同的`xdm:sourceProperty`(`mobile phone`)，並將`xdm:namespace`更改為`Phone`。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**回應**

成功的響應返回HTTP狀態201（已建立）和更新描述符的`@id`（應與請求中發送的`@id`匹配）。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

執行[查閱(GET)請求](#lookup)以檢視描述符時，會顯示欄位已更新，以反映在PUT請求中傳送的變更。

## 刪除描述符{#delete}

有時，您可能需要刪除從[!DNL Schema Registry]中定義的描述符。 通過引用要刪除的描述符的`@id`進行DELETE請求來完成此操作。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要刪除的描述符的`@id`。 |

**要求**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白的內文。

要確認描述符已刪除，可以對描述符`@id`執行[查找請求](#lookup)。 響應返回HTTP狀態404（找不到），因為描述符已從[!DNL Schema Registry]中刪除。

## 附錄

以下部分提供有關在[!DNL Schema Registry] API中使用描述符的其他資訊。

### 定義描述符{#defining-descriptors}

以下各節概述了可用描述符類型，包括定義每種類型描述符的必需欄位。

#### 身份描述符

身份描述符發出信號，表示&quot;[!UICONTROL sourceSchema]&quot;的&quot;[!UICONTROL sourceProperty]&quot;是[!DNL Identity]欄位，如[Adobe Experience Platform身份服務](../../identity-service/home.md)所述。

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| 屬性 | 說明 |
| --- | --- |
| `@type` | 正在定義的描述符類型。 |
| `xdm:sourceSchema` | 定義描述符的架構的`$id` URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 將作為身份的特定屬性的路徑。 路徑應以&quot;/&quot;開頭，而不以&quot;/&quot;結束。 路徑中不包含「屬性」（例如，使用「/personalEmail/address」而非「/properties/personalEmail/properties/address」） |
| `xdm:namespace` | 識別名稱空間的`id`或`code`值。 使用[[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)可找到名稱空間清單。 |
| `xdm:property` | 根據使用的`xdm:namespace`，可選擇`xdm:id`或`xdm:code`。 |
| `xdm:isPrimary` | 選用的布林值。 若為true，則將欄位指示為主要身分。 結構只能包含一個主要標識。 |

#### 友好名稱描述符

友好的名稱描述符允許用戶修改核心庫模式欄位的`title`、`description`和`meta:enum`值。 當使用您想要標示為包含您組織特定資訊的「eVar」和其他「一般」欄位時，特別有用。 UI可使用這些來顯示更好記的名稱，或僅顯示具有好記名稱的欄位。

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `@type` | 正在定義的描述符類型。 |
| `xdm:sourceSchema` | 定義描述符的架構的`$id` URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 將作為身份的特定屬性的路徑。 路徑應以&quot;/&quot;開頭，而不以&quot;/&quot;結束。 路徑中不包含「屬性」（例如，使用「/personalEmail/address」而非「/properties/personalEmail/properties/address」） |
| `xdm:title` | 您要為此欄位顯示的新標題，在「標題大小寫」中撰寫。 |
| `xdm:description` | 可隨標題新增選擇性說明。 |
| `meta:enum` | 如果`xdm:sourceProperty`所指示的欄位是字串欄位，`meta:enum`會決定[!DNL Experience Platform] UI中欄位的建議值清單。 請務必注意，`meta:enum`不聲明枚舉或為XDM欄位提供任何資料驗證。<br><br>這僅應用於由Adobe定義的核心XDM欄位。如果source屬性是您組織定義的自訂欄位，則您應直接透過欄位父資源的PATCH請求編輯欄位的`meta:enum`屬性。 |

#### 關係描述子

關係描述符描述了兩個不同模式之間的關係，它們基於`sourceProperty`和`destinationProperty`中描述的屬性進行鍵入。 有關詳細資訊，請參閱[中的教程，該教程定義兩個方案之間的關係。](../tutorials/relationship-api.md)

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| 屬性 | 說明 |
| --- | --- |
| `@type` | 正在定義的描述符類型。 |
| `xdm:sourceSchema` | 定義描述符的架構的`$id` URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 定義關係的源架構中欄位的路徑。 應以&quot;/&quot;開頭，而非以&quot;/&quot;結尾。 不要在路徑中包含「屬性」（例如，「/personalEmail/address」，而不是「/properties/personalEmail/properties/address」）。 |
| `xdm:destinationSchema` | 此描述符正在定義與的目標模式的`$id` URI。 |
| `xdm:destinationVersion` | 目標架構的主要版本。 |
| `xdm:destinationProperty` | 目標方案內目標欄位的可選路徑。 如果省略此屬性，則目標欄位由包含匹配引用標識描述符的任何欄位推斷（請參見下面）。 |


#### 參考身份描述符

參考標識描述符為模式欄位的主標識提供參考上下文，允許其他模式中的欄位引用它。 在將引用描述符應用到這些欄位之前，必須已使用標識描述符標籤欄位。

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| 屬性 | 說明 |
| --- | --- |
| `@type` | 正在定義的描述符類型。 |
| `xdm:sourceSchema` | 定義描述符的架構的`$id` URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 定義描述符的源模式中欄位的路徑。 應以&quot;/&quot;開頭，而非以&quot;/&quot;結尾。 不要在路徑中包含「屬性」（例如，「/personalEmail/address」，而不是「/properties/personalEmail/properties/address」）。 |
| `xdm:identityNamespace` | source屬性的識別名稱空間代碼。 |
