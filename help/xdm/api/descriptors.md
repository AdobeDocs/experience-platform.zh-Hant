---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述項；描述項；描述項；描述項；身分；身分；易記名稱；易記名稱；alternatedisplayinfo；參考；參考；關係；關係
solution: Experience Platform
title: 描述項API端點
description: Schema Registry API中的/descriptors端點可讓您以程式設計方式管理體驗應用程式中的XDM描述項。
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 02a22362b9ecbfc5fd7fcf17dc167309a0ea45d5
workflow-type: tm+mt
source-wordcount: '2888'
ht-degree: 1%

---

# 描述項端點

結構描述會定義資料實體的結構，但不會指定從這些結構描述建立的任何資料集如何彼此關聯。 在Adobe Experience Platform中，您可以使用描述元來說明這些關係，並將解譯性中繼資料新增到結構描述。

描述項是套用至Adobe Experience Platform中結構描述的租使用者層級中繼資料物件。 它們定義結構關係、索引鍵和行為欄位（例如時間戳記或版本設定），這些欄位會影響到下游資料的驗證、連結或解譯方式。

結構描述可以有一或多個描述項。 每個描述項都定義了`@type`以及它適用的`sourceSchema`。 描述項會自動套用至從該結構描述建立的所有資料集。

在Adobe Experience Platform中，描述項是將行為規則或結構含義新增到結構描述的中繼資料。
描述項有多種型別，包括：

- [身分描述項](#identity-descriptor) — 將欄位標示為身分
- [主索引鍵描述項](#primary-key-descriptor) — 強制唯一性
- [關聯性描述項](#relationship-descriptor) — 定義外部索引鍵聯結
- [替代顯示資訊描述項](#friendly-name) — 讓您重新命名UI中的欄位
- [版本](#version-descriptor)和[時間戳記](#timestamp-descriptor)描述項 — 追蹤事件順序和變更偵測

`/descriptors` API中的[!DNL Schema Registry]端點可讓您以程式設計方式管理體驗應用程式中的描述項。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)的一部分。 在繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience Platform API所需必要標題的重要資訊。

除了標準描述項之外，[!DNL Schema Registry]還支援模型架構的描述項型別，例如&#x200B;**主索引鍵**、**版本**&#x200B;和&#x200B;**時間戳記**。 這些會強制唯一性、控制版本化，並在架構層級定義時間序列欄位。 如果您不熟悉以模型為基礎的結構描述，請先檢閱[Data Mirror概觀](../data-mirror/overview.md)和[以模型為基礎的結構描述技術參考](../schema/model-based.md)，然後再繼續。

>[!IMPORTANT]
>
>如需所有描述項型別的詳細資訊，請參閱[附錄](#defining-descriptors)。

## 擷取描述項清單 {#list}

您可以藉由向`/tenant/descriptors`發出GET要求，列出貴組織已定義的所有描述項。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

回應格式取決於請求中傳送的`Accept`標頭。 請注意，`/descriptors`端點使用與`Accept` API中所有其他端點不同的[!DNL Schema Registry]標頭。

>[!IMPORTANT]
>
>描述項需要以`Accept`取代`xed`的唯一的`xdm`標頭，並提供描述項唯一的`link`選項。 以下範例呼叫中已包含適當的`Accept`標頭，但請特別注意，以確保在使用描述項時使用正確的標頭。

| `Accept`標題 | 說明 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 傳回描述項ID的陣列 |
| `application/vnd.adobe.xdm-link+json` | 傳回描述項API路徑的陣列 |
| `application/vnd.adobe.xdm+json` | 傳回擴充描述項物件的陣列 |
| `application/vnd.adobe.xdm-v2+json` | 此`Accept`標頭必須使用分頁功能。 |

{style="table-layout:auto"}

**回應**

此回應包括已定義描述元的每個描述項型別的陣列。 換言之，如果沒有定義特定`@type`的描述項，登入將不會傳回該描述項型別的空白陣列。

使用`link` `Accept`標頭時，每個描述項都會以格式`/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`顯示為陣列專案

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

## 查詢描述項 {#lookup}

若要檢視特定描述項的詳細資料，請使用其`@id`傳送GET要求。

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 您要查閱之描述項的`@id`。 |

{style="table-layout:auto"}

**要求**

下列要求會依據其`@id`值擷取描述項。 描述項未建立版本，因此查詢請求中不需要標頭`Accept`。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回描述項的詳細資料，包括其`@type`和`sourceSchema`，以及視描述項型別而異的其他資訊。 傳回的`@id`應該符合要求中提供的描述項`@id`。

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
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 建立描述項 {#create}

您可以對`/tenant/descriptors`端點發出POST要求，以建立新的描述項。

>[!IMPORTANT]
>
>[!DNL Schema Registry]可讓您定義數個不同的描述項型別。 每個描述項型別都需要在請求內文中傳送其專屬的特定欄位。 請參閱[附錄](#defining-descriptors)，以取得描述元的完整清單以及定義描述元所需的欄位。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求在範例結構描述中的「電子郵件地址」欄位上定義身分描述項。 這會告訴[!DNL Experience Platform]使用電子郵件地址做為識別碼，以協助彙整個人的資訊。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的回應會傳回HTTP狀態201 （已建立）和新建立之描述項的詳細資料，包括其`@id`。 `@id`是由[!DNL Schema Registry]指派的唯讀欄位，用於參考API中的描述項。

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

## 更新描述項 {#put}

您可以在PUT要求的路徑中包含描述項的`@id`以更新描述項。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 您要更新的描述項的`@id`。 |

{style="table-layout:auto"}

**要求**

此請求基本上會重寫描述項，因此請求內文必須包含定義該型別描述項所需的所有欄位。 換句話說，更新(PUT)描述項的要求承載與[建立相同型別(POST)描述項](#create)的承載相同。

>[!IMPORTANT]
>
>與使用POST要求建立描述項一樣，每種描述項型別都需要在PUT要求裝載中傳送其專屬欄位。 請參閱[附錄](#defining-descriptors)，以取得描述元的完整清單以及定義描述元所需的欄位。

下列範例會更新身分描述項以參考其他`xdm:sourceProperty` (`mobile phone`)，並將`xdm:namespace`變更為`Phone`。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的回應會傳回HTTP狀態201 （已建立）和更新描述項的`@id` （應該符合要求中傳送的`@id`）。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

執行[查詢(GET)要求](#lookup)以檢視描述項，會顯示欄位現已更新，以反映PUT要求中傳送的變更。

## 刪除描述項 {#delete}

有時您可能需要從[!DNL Schema Registry]中移除已定義的描述項。 這可透過發出DELETE請求來完成，該請求會參考您要移除之描述項的`@id`。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 您要刪除之描述項的`@id`。 |

{style="table-layout:auto"}

**要求**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

若要確認描述項已刪除，您可以對描述項[執行](#lookup)查詢要求`@id`。 回應傳回HTTP狀態404 （找不到），因為描述項已從[!DNL Schema Registry]中移除。

## 附錄 {#appendix}

下節提供有關在[!DNL Schema Registry] API中使用描述項的其他資訊。

### 定義描述項 {#defining-descriptors}

>[!NOTE]
>
>可套用至組織沙箱的描述項數目上限為4000。

以下小節提供可用描述項型別的概觀，包括定義每種型別的描述項所需的欄位。

>[!IMPORTANT]
>
>您無法標籤租使用者名稱空間物件，因為系統會將該標籤套用至該沙箱中的每個自訂欄位。 反之，您必須在該物件下指定需要加上標籤的分葉節點。

#### 身分描述項 {#identity-descriptor}

身分描述項會指出「[!UICONTROL sourceSchema]」的「[!UICONTROL sourceProperty]」是[!DNL Identity]Experience Platform Identity Service[所說明的](../../identity-service/home.md)欄位。

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
| `@type` | 正在定義的描述項型別。 對於身分描述項，此值必須設定為`xdm:descriptorIdentity`。 |
| `xdm:sourceSchema` | 正在定義描述項的結構描述的`$id` URI。 |
| `xdm:sourceVersion` | 來源結構描述的主要版本。 |
| `xdm:sourceProperty` | 將成為身分的特定屬性的路徑。 路徑應該以「/」開頭，而不是以開頭。 不要在路徑中包含「properties」（例如，使用「/personalEmail/address」而非「/properties/personalEmail/properties/address」） |
| `xdm:namespace` | 身分名稱空間的`id`或`code`值。 可使用[[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service)找到名稱空間清單。 |
| `xdm:property` | 視使用的`xdm:id`而定，`xdm:code`或`xdm:namespace`。 |
| `xdm:isPrimary` | 選用的布林值。 為true時，將欄位指示為主要身分。 結構描述只能包含一個主要身分。 |

{style="table-layout:auto"}

#### 易記名稱描述項 {#friendly-name}

好記名稱描述元可讓使用者修改核心程式庫結構描述欄位的`title`、`description`和`meta:enum`值。 在使用「eVars」和您希望標示為包含組織特定資訊的其他「一般」欄位時，這個功能特別實用。 UI可利用這些來顯示更好記的名稱，或只顯示具有更好記名稱的欄位。

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
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `@type` | 正在定義的描述項型別。 對於易記名稱描述項，此值必須設定為`xdm:alternateDisplayInfo`。 |
| `xdm:sourceSchema` | 正在定義描述項的結構描述的`$id` URI。 |
| `xdm:sourceVersion` | 來源結構描述的主要版本。 |
| `xdm:sourceProperty` | 您要修改其詳細資訊之特定屬性的路徑。 路徑應該以斜線(`/`)開頭，而不是以一個結尾。 不要在路徑中包含`properties` （例如，使用`/personalEmail/address`而非`/properties/personalEmail/properties/address`）。 |
| `xdm:title` | 您希望為此欄位顯示的新標題，以字首大寫字母撰寫。 |
| `xdm:description` | 可以在標題中新增選用的說明。 |
| `meta:enum` | 如果`xdm:sourceProperty`指示的欄位是字串欄位，則可以使用`meta:enum`在分段UI中為欄位新增建議值。 請務必注意，`meta:enum`不會宣告分項清單或為XDM欄位提供任何資料驗證。<br><br>這僅能用於Adobe定義的核心XDM欄位。 如果來源屬性是您的組織定義的自訂欄位，您應該直接透過欄位父級資源的PATCH請求來編輯欄位的`meta:enum`屬性。 |
| `meta:excludeMetaEnum` | 如果`xdm:sourceProperty`所指示的欄位是字串欄位，其在`meta:enum`欄位下提供了現有的建議值，您可以在易記名稱描述項中加入此物件，以從分段中排除這些值的部分或全部。 每個專案的索引鍵和值都必須與欄位原始`meta:enum`中包含的專案相符，才能排除該專案。 |

{style="table-layout:auto"}

#### 關係描述項 {#relationship-descriptor}

關聯性描述項描述兩個不同結構描述之間的關係，以`xdm:sourceProperty`和`xdm:destinationProperty`中描述的屬性作為索引鍵。 如需詳細資訊，請參閱有關[定義兩個結構描述](../tutorials/relationship-api.md)之間關係的教學課程。

使用這些屬性來宣告來源欄位（外部索引鍵）與目的地欄位（[主索引鍵](#primary-key-descriptor)或候選索引鍵）的關聯方式。

>[!TIP]
>
>**外部索引鍵**&#x200B;是來源結構描述中的欄位（由`xdm:sourceProperty`定義），它參考另一個結構描述中的索引鍵欄位。 **候選索引鍵**&#x200B;是目的地結構描述中唯一識別記錄的任何欄位（或欄位集），可用來取代主索引鍵。

API支援兩種模式：

- `xdm:descriptorOneToOne`：標準1:1關聯性。
- `xdm:descriptorRelationship`：新工作和模型型結構描述的一般模式（支援基數、命名和非主索引鍵目標）。

##### 一對一關係（標準結構描述）

在維護已依賴`xdm:descriptorOneToOne`的現有標準結構描述整合時，請使用此專案。

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

下表說明定義一對一關係描述項所需的欄位。

| 屬性 | 說明 |
| --- | --- |
| `@type` | 正在定義的描述項型別。 對於關係描述項，除非您擁有Real-Time CDP B2B edition的存取權，否則此值必須設定為`xdm:descriptorOneToOne`。 使用B2B edition時，您可以選擇使用`xdm:descriptorOneToOne`或[`xdm:descriptorRelationship`](#b2b-relationship-descriptor)。 |
| `xdm:sourceSchema` | 正在定義描述項的結構描述的`$id` URI。 |
| `xdm:sourceVersion` | 來源結構描述的主要版本。 |
| `xdm:sourceProperty` | 來源結構描述中定義關係的欄位路徑。 開頭應為&quot;/&quot;，結尾應為&quot;/&quot;。 請勿在路徑中包含「properties」（例如，「/personalEmail/address」而非「/properties/personalEmail/properties/address」）。 |
| `xdm:destinationSchema` | 此描述項正在定義關聯性的參考結構描述的`$id` URI。 |
| `xdm:destinationVersion` | 參考結構描述的主要版本。 |
| `xdm:destinationProperty` | （選用）參照結構描述中目標欄位的路徑。 如果省略此屬性，則任何包含相符參考身分描述項的欄位都會推斷目標欄位（請參閱下文）。 |

##### 一般關係（以模型為基礎的結構描述，以及新專案的建議使用）

請將此描述項用於所有新實作和模型型結構描述。 它可讓您定義關係的基數（例如一對一或多對一）、指定關係名稱，以及連結至非主索引鍵（非主索引鍵）的目的地欄位。

下列範例顯示如何定義一般關係描述項。

**最小範例：**

這個最小範例僅包含定義兩個結構描述之間多對一關係的必填欄位。

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceProperty": "/customer_ref",
  "xdm:sourceVersion": 1,
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:cardinality": "M:1"
}
```

**所有選擇性欄位的範例：**

此範例包含所有選擇性欄位，例如關係名稱、顯示標題和明確的非主索引鍵目的地欄位。

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/customer_ref",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationProperty": "/customer_id",
  "xdm:sourceToDestinationName": "CampaignToCustomer",
  "xdm:destinationToSourceName": "CustomerToCampaign",
  "xdm:sourceToDestinationTitle": "Customer campaigns",
  "xdm:destinationToSourceTitle": "Campaign customers",
  "xdm:cardinality": "M:1"
}
```

##### 選擇關係描述項

使用下列准則來決定要套用的關係描述項：

| 狀況 | 要使用的描述項 |
| --------------------------------------------------------------------- | ----------------------------------------- |
| 新的工作或模型架構 | `xdm:descriptorRelationship` |
| 標準結構描述中的現有1:1對應 | 繼續使用`xdm:descriptorOneToOne`，除非您只需要`xdm:descriptorRelationship`支援的功能。 |
| 需要多對一或選用的基數(`1:1`， `1:0`， `M:1`， `M:0`) | `xdm:descriptorRelationship` |
| UI/下游可讀性需要關係名稱或標題 | `xdm:descriptorRelationship` |
| 需要不是身分的目的地目標 | `xdm:descriptorRelationship` |

>[!NOTE]
>
>對於標準結構描述中的現有`xdm:descriptorOneToOne`描述項，除非您需要非主要身分目的地目標、自訂命名或擴充基數選項等功能，否則請繼續使用它們。

##### 功能比較

下表比較兩種描述項型別的功能：

| 功能 | `xdm:descriptorOneToOne` | `xdm:descriptorRelationship` |
| ------------------ | ------------------------ | ------------------------------------------------------------------------ |
| 基數 | 1:1 | 1:1， 1:0， M:1， M:0 （資訊） |
| 目的地目標 | 身分/明確欄位 | 預設主索引鍵，或透過`xdm:destinationProperty`的非主索引鍵 |
| 命名欄位 | 不支援 | `xdm:sourceToDestinationName`、`xdm:destinationToSourceName`和標題 |
| 關聯式符合 | 有限 | 模型型結構描述的主要模式 |

##### 限制和驗證

定義一般關係描述項時，請遵循下列需求和建議：

- 對於以模型為基礎的結構描述，請將來源欄位（外部索引鍵）放置在根層級。 這是目前擷取的技術限制，並非最佳實務建議。
- 確保來源和目的地欄位的資料型別相容（數值、日期、布林值、字串）。
- 請記住，基數僅供參考；儲存不會強制執行。 以`<source>:<destination>`格式指定基數。 接受的值為： `1:1`、`1:0`、`M:1`或`M:0`。

#### 主索引鍵描述項 {#primary-key-descriptor}

主索引鍵描述項(`xdm:descriptorPrimaryKey`)在結構描述中的一或多個欄位上強制唯一性和非null限制。

```json
{
  "@type": "xdm:descriptorPrimaryKey",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": ["/orderId", "/orderLineId"]
}
```

| 屬性 | 說明 |
| -------------------- | ----------------------------------------------------------------------------- |
| `@type` | 必須為`xdm:descriptorPrimaryKey`。 |
| `xdm:sourceSchema` | 結構描述的`$id` URI。 |
| `xdm:sourceProperty` | 主鍵欄位的JSON指標。 使用複合鍵的陣列。 對於時間序列結構描述，複合金鑰必須包含時間戳記欄位，以確保事件記錄之間的唯一性。 |

#### 版本描述項 {#version-descriptor}

>[!NOTE]
>
>在UI結構描述編輯器中，版本描述項顯示為&quot;[!UICOTRNOL 版本識別碼]&quot;。

版本描述項(`xdm:descriptorVersion`)會指定一個欄位，以偵測並防止順序錯亂的變更事件發生衝突。

```json
{
  "@type": "xdm:descriptorVersion",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/versionNumber"
}
```

| 屬性 | 說明 |
| -------------------- | ------------------------------------------------------------- |
| `@type` | 必須為`xdm:descriptorVersion`。 |
| `xdm:sourceSchema` | 結構描述的`$id` URI。 |
| `xdm:sourceProperty` | 版本欄位的JSON指標。 必須標籤為`required`。 |

#### 時間戳記描述項 {#timestamp-descriptor}

>[!NOTE]
>
>在UI結構描述編輯器中，時間戳記描述項會顯示為&quot;[!UICOTRNOL 時間戳記識別碼]&quot;。

時間戳記描述項(`xdm:descriptorTimestamp`)指定日期 — 時間欄位做為具有`"meta:behaviorType": "time-series"`的結構描述的時間戳記。

```json
{
  "@type": "xdm:descriptorTimestamp",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/eventTime"
}
```

| 屬性 | 說明 |
| -------------------- | ------------------------------------------------------------------------------------------ |
| `@type` | 必須為`xdm:descriptorTimestamp`。 |
| `xdm:sourceSchema` | 結構描述的`$id` URI。 |
| `xdm:sourceProperty` | JSON時間戳記欄位指標。 必須標示為`required`且型別為`date-time`。 |

##### B2B關係描述項 {#B2B-relationship-descriptor}

Real-Time CDP B2B edition引進了定義結構描述之間關係的替代方式，其允許多對一關係。 此新關聯性必須具有`@type: xdm:descriptorRelationship`型別，而且裝載必須包含比`@type: xdm:descriptorOneToOne`關聯性更多的欄位。 如需詳細資訊，請參閱有關[定義B2B edition](../tutorials/relationship-b2b.md)的結構描述關係的教學課程。

```json
{
   "@type": "xdm:descriptorRelationship",
   "xdm:sourceSchema" : "https://ns.adobe.com/{TENANT_ID}/schemas/9f2b2f225ac642570a110d8fd70800ac0c0573d52974fa9a",
   "xdm:sourceVersion" : 1,
   "xdm:sourceProperty" : "/person-ref",
   "xdm:destinationSchema" : "https://ns.adobe.com/{TENANT_ID/schemas/628427680e6b09f1f5a8f63ba302ee5ce12afba8de31acd7",
   "xdm:destinationVersion" : 1,
   "xdm:destinationProperty": "/personId",
   "xdm:destinationNamespace" : "People", 
   "xdm:destinationToSourceTitle" : "Opportunity Roles",
   "xdm:sourceToDestinationTitle" : "People",
   "xdm:cardinality": "M:1"
}
```

| 屬性 | 說明 |
| --- | --- |
| `@type` | 正在定義的描述項型別。 對於具有下列欄位的我們，值必須設定為`xdm:descriptorRelationship`。 如需其他型別的詳細資訊，請參閱[關聯性描述元](#relationship-descriptor)區段。 |
| `xdm:sourceSchema` | 正在定義描述項的結構描述的`$id` URI。 |
| `xdm:sourceVersion` | 來源結構描述的主要版本。 |
| `xdm:sourceProperty` | 來源結構描述中定義關係的欄位路徑。 開頭應為&quot;/&quot;，結尾應為&quot;/&quot;。 請勿在路徑中包含「properties」（例如，「/personalEmail/address」而非「/properties/personalEmail/properties/address」）。 |
| `xdm:destinationSchema` | 此描述項正在定義關聯性的參考結構描述的`$id` URI。 |
| `xdm:destinationVersion` | 參考結構描述的主要版本。 |
| `xdm:destinationProperty` | （選用）參照結構描述中目標欄位的路徑。 這必須解析為結構描述的主要ID，或解析為另一個具有相容資料型別的欄位至`xdm:sourceProperty`。 如果省略，此關係可能無法如預期運作。 |
| `xdm:destinationNamespace` | 參照結構描述中的主要ID名稱空間。 |
| `xdm:destinationToSourceTitle` | 從參考結構描述到來源結構描述的關係顯示名稱。 |
| `xdm:sourceToDestinationTitle` | 從來源結構描述到參考結構描述的關係顯示名稱。 |
| `xdm:cardinality` | 結構描述之間的結合關係。 此值應設為`M:1`，表示多對一關係。 |

{style="table-layout:auto"}

#### 參考身分描述項

參考身分描述項提供結構描述欄位主要身分的參考內容，讓其他結構描述中的欄位可參考內容。 參考結構描述必須先定義主要身分欄位，其他結構描述才能透過此描述項參考它。

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
| `@type` | 正在定義的描述項型別。 對於參考身分描述項，此值必須設定為`xdm:descriptorReferenceIdentity`。 |
| `xdm:sourceSchema` | 正在定義描述項的結構描述的`$id` URI。 |
| `xdm:sourceVersion` | 來源結構描述的主要版本。 |
| `xdm:sourceProperty` | 來源結構描述中用於參考參考結構描述的欄位路徑。 應該以「/」開頭，而不是以開頭。 請勿在路徑中包含「屬性」（例如，`/personalEmail/address`而非`/properties/personalEmail/properties/address`）。 |
| `xdm:identityNamespace` | 來源屬性的身分名稱空間程式碼。 |

{style="table-layout:auto"}

#### 已棄用的欄位描述項

您可以將設定為[的](../tutorials/field-deprecation-api.md#custom)屬性新增至有問題的欄位，以`meta:status`棄用自訂XDM資源`deprecated`中的欄位。 不過，如果您想要取代結構描述中標準XDM資源提供的欄位，您可以將取代的欄位描述項指派給相關結構描述，以取得相同的效果。 使用[正確的`Accept`標頭](../tutorials/field-deprecation-api.md#verify-deprecation)，您就可以在API中查詢結構描述時，檢視該結構描述已棄用的標準欄位。

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| 屬性 | 說明 |
| --- | --- |
| `@type` | 描述項的型別。 對於欄位取代描述項，此值必須設定為`xdm:descriptorDeprecated`。 |
| `xdm:sourceSchema` | 您要套用描述項之結構描述的URI `$id`。 |
| `xdm:sourceVersion` | 您要套用描述項的結構描述版本。 應該設定為`1`。 |
| `xdm:sourceProperty` | 在要套用描述項的結構描述中，屬性的路徑。 如果您想要將描述項套用至多個屬性，可以陣列形式提供路徑清單（例如，`["/firstName", "/lastName"]`）。 |

{style="table-layout:auto"}
