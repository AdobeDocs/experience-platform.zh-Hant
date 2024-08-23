---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述項；描述項；描述項；描述項；身分；身分；易記名稱；易記名稱；alternatedisplayinfo；參考；參考；關係；關係
solution: Experience Platform
title: 描述項API端點
description: Schema Registry API中的/descriptors端點可讓您以程式設計方式管理體驗應用程式中的XDM描述項。
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 866e00459c66ea4678cd98d119a7451fd8e78253
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 1%

---

# 描述項端點

結構描述會定義資料實體的靜態檢視，但不會提供這些結構描述（例如資料集）所依據的資料如何彼此關聯的特定詳細資訊。 Adobe Experience Platform可讓您使用描述項描述這些關係以及有關結構描述的其他可解譯的中繼資料。

結構描述項是租使用者層級的中繼資料，這表示它們對於您的組織都是唯一的，並且所有描述項作業都在租使用者容器中進行。

每個結構描述可以套用一或多個結構描述項實體。 每個結構描述描述項實體都包含描述項`@type`及其適用的`sourceSchema`。 套用後，這些描述項將套用至使用結構描述建立的所有資料集。

[!DNL Schema Registry] API中的`/descriptors`端點可讓您以程式設計方式管理體驗應用程式中的描述項。

## 快速入門

本指南中使用的端點是[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)的一部分。 繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

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

回應格式取決於請求中傳送的`Accept`標頭。 請注意，`/descriptors`端點使用與[!DNL Schema Registry] API中所有其他端點不同的`Accept`標頭。

>[!IMPORTANT]
>
>描述項需要以`xdm`取代`xed`的唯一的`Accept`標頭，並提供描述項唯一的`link`選項。 以下範例呼叫中已包含適當的`Accept`標頭，但請特別注意，以確保在使用描述項時使用正確的標頭。

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

如果您想要檢視特定描述項的詳細資訊，可以使用其`@id`來查詢(GET)個別描述項。

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

此請求基本上會重寫描述項，因此請求內文必須包含定義該型別描述項所需的所有欄位。 換句話說，更新(PUT)描述項的要求承載與[建立(POST)相同型別的描述項](#create)的承載相同。

>[!IMPORTANT]
>
>和使用POST要求建立描述項一樣，每種描述項型別都需要在PUT要求裝載中傳送其專屬欄位。 請參閱[附錄](#defining-descriptors)，以取得描述元的完整清單以及定義描述元所需的欄位。

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

執行[查詢(GET)要求](#lookup)以檢視描述項，顯示欄位現在已更新，以反映PUT要求中傳送的變更。

## 刪除描述項 {#delete}

有時您可能需要從[!DNL Schema Registry]中移除已定義的描述項。 這是透過發出DELETE請求來完成，該請求會參考您要移除之描述項的`@id`。

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

若要確認描述項已刪除，您可以對描述項`@id`執行[查詢要求](#lookup)。 回應傳回HTTP狀態404 （找不到），因為描述項已從[!DNL Schema Registry]中移除。

## 附錄

下節提供有關在[!DNL Schema Registry] API中使用描述項的其他資訊。

### 定義描述項 {#defining-descriptors}

>[!NOTE]
>
>可套用至組織沙箱的描述項數目上限為4000。

以下小節提供可用描述項型別的概觀，包括定義每種型別的描述項所需的欄位。

>[!IMPORTANT]
>
>您無法標籤租使用者名稱空間物件，因為系統會將該標籤套用至該沙箱中的每個自訂欄位。 反之，您必須在該物件下指定需要加上標籤的分葉節點。

#### 身分描述項

身分描述項會指出「[!UICONTROL sourceSchema]」的「[!UICONTROL sourceProperty]」是[Adobe Experience Platform Identity Service](../../identity-service/home.md)所說明的[!DNL Identity]欄位。

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
| `xdm:property` | 視使用的`xdm:namespace`而定，`xdm:id`或`xdm:code`。 |
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

#### 關係描述項

關聯性描述項描述兩個不同結構描述之間的關係，以`sourceProperty`和`destinationProperty`中描述的屬性作為索引鍵。 如需詳細資訊，請參閱有關[定義兩個結構描述](../tutorials/relationship-api.md)之間關係的教學課程。

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
| `@type` | 正在定義的描述項型別。 對於關聯性描述項，此值必須設定為`xdm:descriptorOneToOne`。 |
| `xdm:sourceSchema` | 正在定義描述項的結構描述的`$id` URI。 |
| `xdm:sourceVersion` | 來源結構描述的主要版本。 |
| `xdm:sourceProperty` | 來源結構描述中定義關係的欄位路徑。 應該以「/」開頭，而不是以開頭。 請勿在路徑中包含「properties」（例如，「/personalEmail/address」而非「/properties/personalEmail/properties/address」）。 |
| `xdm:destinationSchema` | 此描述項正在定義關聯性的參考結構描述的`$id` URI。 |
| `xdm:destinationVersion` | 參考結構描述的主要版本。 |
| `xdm:destinationProperty` | 參照結構描述中目標欄位的選用路徑。 如果省略此屬性，則任何包含相符參考身分描述項的欄位都會推斷目標欄位（請參閱下文）。 |

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

您可以將設定為`deprecated`的`meta:status`屬性新增至有問題的欄位，以[棄用自訂XDM資源](../tutorials/field-deprecation-api.md#custom)中的欄位。 不過，如果您想要取代結構描述中標準XDM資源提供的欄位，您可以將取代的欄位描述項指派給相關結構描述，以取得相同的效果。 使用[正確的`Accept`標頭](../tutorials/field-deprecation-api.md#verify-deprecation)，您就可以在API中查詢結構描述時，檢視該結構描述已棄用的標準欄位。

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
