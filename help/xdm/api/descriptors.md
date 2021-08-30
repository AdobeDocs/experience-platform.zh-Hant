---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構登錄；結構登錄；描述元；描述元；描述元；描述元；身分；易記名稱；替代顯示資訊；參考；關係；關係
solution: Experience Platform
title: 描述符API端點
description: Schema Registry API中的/descriptors端點可讓您以程式設計方式管理體驗應用程式中的XDM描述元。
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: f269a7b1584a6e4a0e1820a0c587a647c0c8f7b5
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 3%

---

# 描述符端點

結構會定義資料實體的靜態檢視，但不提供根據這些結構（例如資料集）的資料如何彼此關聯的特定詳細資料。 Adobe Experience Platform可讓您使用描述元來描述這些關係和關於架構的其他解釋性中繼資料。

結構描述元是租戶層級的中繼資料，這表示它們對您的IMS組織是唯一的，所有描述元操作都會在租戶容器中進行。

每個架構都可以應用一個或多個架構描述符實體。 每個架構描述符實體都包含一個描述符`@type`，以及該描述符所應用的`sourceSchema`。 套用後，這些描述元將套用至使用結構建立的所有資料集。

[!DNL Schema Registry] API中的`/descriptors`端點可讓您以程式設計方式管理體驗應用程式中的描述元。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml)的一部分。 繼續之前，請檢閱[快速入門手冊](./getting-started.md)，取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭的重要資訊。

## 檢索描述符清單 {#list}

您可以向`/tenant/descriptors`發出GET請求，以列出您的組織已定義的所有描述符。

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

回應格式取決於要求中傳送的`Accept`標題。 請注意，`/descriptors`端點使用的`Accept`標頭與[!DNL Schema Registry] API中的所有其他端點不同。

>[!IMPORTANT]
>
>描述符需要唯一的`Accept`標頭，該標頭將`xed`替換為`xdm`，並且還提供描述符唯一的`link`選項。 下列範例呼叫中已包含正確的`Accept`標題，但請格外小心，以確保使用描述元時，會使用正確的標題。

| `Accept` 標題 | 說明 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID的陣列 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路徑的陣列 |
| `application/vnd.adobe.xdm+json` | 返回擴展描述符對象的陣列 |
| `application/vnd.adobe.xdm-v2+json` | 必須使用此`Accept`標頭才能使用分頁功能。 |

{style=&quot;table-layout:auto&quot;}

**回應**

該響應包括用於具有定義描述符的每個描述符類型的陣列。 換言之，如果沒有定義的某個`@type`描述符，則註冊表將不會為該描述符類型返回空陣列。

使用`link` `Accept`標頭時，每個描述符都以`/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`格式顯示為陣列項

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

## 查找描述符 {#lookup}

如果要查看特定描述符的詳細資訊，可以使用其`@id`查找(GET)單個描述符。

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要查找的描述符的`@id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求通過其`@id`值檢索描述符。 描述元沒有版本控制，因此查閱請求中不需要`Accept`標題。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回描述符的詳細資訊，包括其`@type`和`sourceSchema`，以及根據描述符的類型而變化的其他資訊。 傳回的`@id`應符合要求中提供的描述元`@id`。

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

## 建立描述符 {#create}

可以通過向`/tenant/descriptors`端點發出POST請求來建立新描述符。

>[!IMPORTANT]
>
>[!DNL Schema Registry]允許您定義多個不同的描述符類型。 每個描述符類型都需要在請求正文中發送其自己的特定欄位。 有關描述符的完整清單以及定義描述符所需的欄位，請參見[附錄](#defining-descriptors)。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求在示例架構的「電子郵件地址」欄位中定義標識描述符。 這會告訴[!DNL Experience Platform]使用電子郵件地址做為識別碼，以協助匯整個人的相關資訊。

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

成功的響應返回HTTP狀態201（已建立）以及新建立描述符的詳細資訊，包括其`@id`。 `@id`是[!DNL Schema Registry]指派的唯讀欄位，用於參考API中的描述符。

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

## 更新描述符 {#put}

您可以在PUT請求的路徑中加入描述符`@id`以更新描述符。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要更新的描述符的`@id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

此請求實際上重寫描述符，因此請求主體必須包含定義該類型描述符所需的所有欄位。 換句話說，用於更新(PUT)描述符的請求裝載與用於建立(POST)相同類型的描述符[的裝載相同。](#create)

>[!IMPORTANT]
>
>與使用POST請求建立描述符一樣，每個描述符類型要求在PUT請求負載中發送其自己的特定欄位。 有關描述符的完整清單以及定義描述符所需的欄位，請參見[附錄](#defining-descriptors)。

以下示例更新標識描述符以引用不同的`xdm:sourceProperty`(`mobile phone`)，並將`xdm:namespace`更改為`Phone`。

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

成功的回應會傳回HTTP狀態201（已建立），以及更新描述元的`@id`（應符合要求中傳送的`@id`）。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

執行[查閱(GET)請求](#lookup)以查看描述符時，將顯示欄位已更新，以反映PUT請求中發送的更改。

## 刪除描述符 {#delete}

有時，您可能需要刪除從[!DNL Schema Registry]中定義的描述符。 要執行此操作，請發出參考要刪除的描述符`@id`的DELETE請求。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要刪除的描述符的`@id`。 |

{style=&quot;table-layout:auto&quot;}

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

成功的回應會傳回HTTP狀態204（無內容）和空白內文。

要確認描述符已刪除，可以對描述符`@id`執行[查找請求](#lookup)。 響應返回HTTP狀態404（找不到），因為描述符已從[!DNL Schema Registry]中刪除。

## 附錄

下節提供了有關在[!DNL Schema Registry] API中使用描述符的其他資訊。

### 定義描述符 {#defining-descriptors}

以下各節提供了可用描述符類型的概述，包括定義每種類型描述符所需的欄位。

#### 身份描述符

標識描述符表示「[!UICONTROL sourceSchema]」的「[!UICONTROL sourceProperty]」是[Adobe Experience Platform Identity Service](../../identity-service/home.md)所述的[!DNL Identity]欄位。

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
| `@type` | 要定義的描述符的類型。 |
| `xdm:sourceSchema` | 定義描述符的架構的`$id` URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 將作為身分的特定屬性的路徑。 路徑應以「/」開頭，而非以「/」結尾。 請勿在路徑中加入「屬性」（例如使用「/personalEmail/address」而非「/properties/personalEmail/properties/address」） |
| `xdm:namespace` | 身分識別命名空間的`id`或`code`值。 可使用[[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service)找到命名空間清單。 |
| `xdm:property` | 視使用的`xdm:namespace`而定，可以是`xdm:id`或`xdm:code`。 |
| `xdm:isPrimary` | 選用的布林值。 若為true，則將欄位指示為主要身分。 結構只能包含一個主要身分。 |

{style=&quot;table-layout:auto&quot;}

#### 友好名稱描述符

易記名稱描述符允許用戶修改核心庫架構欄位的`title`、`description`和`meta:enum`值。 在使用「eVar」和其他「一般」欄位時特別實用，您要將這些欄位標示為包含貴組織專屬資訊。 UI可使用這些來顯示更好記的名稱，或只顯示具有好記名稱的欄位。

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
| `@type` | 要定義的描述符的類型。 |
| `xdm:sourceSchema` | 定義描述符的架構的`$id` URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 將作為身分的特定屬性的路徑。 路徑應以「/」開頭，而非以「/」結尾。 請勿在路徑中加入「屬性」（例如使用「/personalEmail/address」而非「/properties/personalEmail/properties/address」） |
| `xdm:title` | 您要為此欄位顯示的新標題，寫在標題案例中。 |
| `xdm:description` | 可新增選用說明及標題。 |
| `meta:enum` | 如果`xdm:sourceProperty`所指示的欄位是字串欄位，`meta:enum`將確定[!DNL Experience Platform] UI中欄位的建議值清單。 請務必注意，`meta:enum`不會宣告分項清單，或不會為XDM欄位提供任何資料驗證。<br><br>此欄位僅應用於Adobe定義的核心XDM欄位。如果來源屬性是貴組織定義的自訂欄位，則您應直接透過對欄位父資源的PATCH請求編輯欄位的`meta:enum`屬性。 |

{style=&quot;table-layout:auto&quot;}

#### 關係描述符

關係描述符描述了兩種不同架構之間的關係，它們以`sourceProperty`和`destinationProperty`中描述的屬性為輸入。 如需詳細資訊，請參閱[定義兩個結構之間關係的教學課程](../tutorials/relationship-api.md)。

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
| `@type` | 要定義的描述符的類型。 |
| `xdm:sourceSchema` | 定義描述符的架構的`$id` URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 定義關係的源架構中欄位的路徑。 應以「/」開頭，而非以「/」結尾。 請勿在路徑中包含「properties」（例如「/personalEmail/address」，而非「/properties/personalEmail/properties/address」）。 |
| `xdm:destinationSchema` | 此描述符正在定義與的關係的目標架構的`$id` URI。 |
| `xdm:destinationVersion` | 目標架構的主要版本。 |
| `xdm:destinationProperty` | 目標架構內目標欄位的可選路徑。 如果省略此屬性，則目標欄位將由包含匹配引用標識描述符的任何欄位推斷（請參見下面）。 |

{style=&quot;table-layout:auto&quot;}


#### 引用標識描述符

參考身份描述符提供指向架構欄位主要身份的參考上下文，允許其他架構中的欄位引用它。 必須先用標識描述符標籤欄位，才能將引用描述符應用到這些欄位。

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
| `@type` | 要定義的描述符的類型。 |
| `xdm:sourceSchema` | 定義描述符的架構的`$id` URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 定義描述符的源架構中欄位的路徑。 應以「/」開頭，而非以「/」結尾。 請勿在路徑中包含「properties」（例如「/personalEmail/address」，而非「/properties/personalEmail/properties/address」）。 |
| `xdm:identityNamespace` | 原始碼屬性的身份命名空間代碼。 |
