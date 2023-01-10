---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構登錄；結構登錄；描述元；描述元；描述元；描述元；身分；易記名稱；替代顯示資訊；參考；關係；關係
solution: Experience Platform
title: 描述符API端點
description: Schema Registry API中的/descriptors端點可讓您以程式設計方式管理體驗應用程式中的XDM描述元。
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1900'
ht-degree: 3%

---

# 描述符端點

結構會定義資料實體的靜態檢視，但不提供根據這些結構（例如資料集）的資料如何彼此關聯的特定詳細資料。 Adobe Experience Platform可讓您使用描述元來描述這些關係和關於架構的其他解釋性中繼資料。

結構描述元是租戶層級的中繼資料，這表示它們對您的IMS組織是唯一的，所有描述元操作都會在租戶容器中進行。

每個架構都可以應用一個或多個架構描述符實體。 每個架構描述符實體包括描述符 `@type` 和 `sourceSchema` 適用。 套用後，這些描述元將套用至使用結構建立的所有資料集。

此 `/descriptors` 端點 [!DNL Schema Registry] API可讓您以程式設計方式管理體驗應用程式中的描述元。

## 快速入門

本指南中使用的端點屬於 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

## 檢索描述符清單 {#list}

您可以向發出GET請求，以列出組織已定義的所有描述元 `/tenant/descriptors`.

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

回應格式取決於 `Accept` 請求中傳送的標題。 請注意， `/descriptors` 端點使用 `Accept` 與中所有其他端點不同的標題 [!DNL Schema Registry] API。

>[!IMPORTANT]
>
>描述符需要唯一 `Accept` 標題取代 `xed` with `xdm`，也提供 `link` 描述符唯一的選項。 正確 `Accept` 標題已包含在下列範例呼叫中，但請格外小心，以確保在使用描述元時，會使用正確的標題。

| `Accept` 標題 | 說明 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID的陣列 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路徑的陣列 |
| `application/vnd.adobe.xdm+json` | 返回擴展描述符對象的陣列 |
| `application/vnd.adobe.xdm-v2+json` | 此 `Accept` 必須使用報頭才能使用分頁功能。 |

{style=&quot;table-layout:auto&quot;}

**回應**

該響應包括用於具有定義描述符的每個描述符類型的陣列。 換句話說，如果沒有某個 `@type` 已定義，註冊表將不會為該描述符類型返回空陣列。

使用 `link` `Accept` 標題，則每個描述符以格式顯示為陣列項 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

如果要查看特定描述符的詳細資訊，可以使用其查找(GET)單個描述符 `@id`.

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 此 `@id` 你要查找的描述符。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求將按其檢索描述符 `@id` 值。 描述符未版本化，因此沒有 `Accept` 查閱請求中需要標題。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回描述符的詳細資訊，包括其 `@type` 和 `sourceSchema`，以及根據描述符類型而變化的其他資訊。 傳回 `@id` 應與描述符匹配 `@id` 於要求中提供。

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

## 建立描述符 {#create}

您可以向發出POST要求，以建立新描述元 `/tenant/descriptors` 端點。

>[!IMPORTANT]
>
>此 [!DNL Schema Registry] 允許您定義多個不同的描述符類型。 每個描述符類型都需要在請求正文中發送其自己的特定欄位。 請參閱 [附錄](#defining-descriptors) 以獲取描述符的完整清單以及定義它們所需的欄位。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求在示例架構的「電子郵件地址」欄位中定義標識描述符。 這說明 [!DNL Experience Platform] 以使用電子郵件地址作為識別碼，協助匯整個人的相關資訊。

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

成功的響應返回HTTP狀態201（已建立）以及新建立描述符的詳細資訊，包括其 `@id`. 此 `@id` 是指派的唯讀欄位 [!DNL Schema Registry] 和，用於參考API中的描述元。

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

可以通過包含描述符來更新描述符 `@id` 在PUT請求的路徑中。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 此 `@id` 要更新的描述符。 |

{style=&quot;table-layout:auto&quot;}

**要求**

此請求實際上重寫描述符，因此請求主體必須包含定義該類型描述符所需的所有欄位。 換言之，要更新(PUT)描述元的請求裝載與要更新的裝載相同 [建立(POST)描述符](#create) 相同類型。

>[!IMPORTANT]
>
>與使用POST請求建立描述符一樣，每個描述符類型要求在PUT請求負載中發送其自己的特定欄位。 請參閱 [附錄](#defining-descriptors) 以獲取描述符的完整清單以及定義它們所需的欄位。

以下示例更新標識描述符以引用不同的 `xdm:sourceProperty` (`mobile phone`)並變更 `xdm:namespace` to `Phone`.

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

成功的回應會傳回HTTP狀態201（已建立），而 `@id` (應與 `@id` 在要求中傳送)。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

執行 [查閱(GET)請求](#lookup) 要查看描述符，將顯示欄位已更新，以反映在PUT請求中發送的更改。

## 刪除描述符 {#delete}

有時，您可能需要從 [!DNL Schema Registry]. 若要這麼做，請提出參考的DELETE請求 `@id` 要刪除的描述符。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 此 `@id` 刪除描述符。 |

{style=&quot;table-layout:auto&quot;}

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

成功的回應會傳回HTTP狀態204（無內容）和空白內文。

要確認描述符已被刪除，可以執行 [查閱請求](#lookup) 對象 `@id`. 響應返回HTTP狀態404（未找到），因為描述符已從 [!DNL Schema Registry].

## 附錄

以下章節提供有關在 [!DNL Schema Registry] API。

### 定義描述符 {#defining-descriptors}

以下各節提供了可用描述符類型的概述，包括定義每種類型描述符所需的欄位。

#### 身份描述符

標識描述符表示[!UICONTROL sourceProperty]&quot;[!UICONTROL sourceSchema]&quot;是 [!DNL Identity] 欄位，如 [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `@type` | 要定義的描述符的類型。 對於標識描述符，此值必須設定為 `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | 此 `$id` 定義描述符的架構的URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 將作為身分的特定屬性的路徑。 路徑應以「/」開頭，而非以「/」結尾。 請勿在路徑中加入「屬性」（例如使用「/personalEmail/address」而非「/properties/personalEmail/properties/address」） |
| `xdm:namespace` | 此 `id` 或 `code` 身分識別命名空間的值。 您可以使用 [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). |
| `xdm:property` | 其中 `xdm:id` 或 `xdm:code`，視 `xdm:namespace` 已使用。 |
| `xdm:isPrimary` | 選用的布林值。 若為true，則將欄位指示為主要身分。 結構只能包含一個主要身分。 |

{style=&quot;table-layout:auto&quot;}

#### 友好名稱描述符 {#friendly-name}

好記的名稱描述元可讓使用者修改 `title`, `description`，和 `meta:enum` 核心程式庫結構欄位的值。 在使用「eVar」和其他「一般」欄位時特別實用，您要將這些欄位標示為包含貴組織專屬資訊。 UI可使用這些來顯示更好記的名稱，或只顯示具有好記名稱的欄位。

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
| `@type` | 要定義的描述符的類型。 對於好記的名稱描述符，此值必須設定為 `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | 此 `$id` 定義描述符的架構的URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 要修改其詳細資訊的特定屬性的路徑。路徑應以斜線(`/`)，而且不以一結尾。 不包括 `properties` 在路徑中(例如，使用 `/personalEmail/address` 而非 `/properties/personalEmail/properties/address`)。 |
| `xdm:title` | 您要為此欄位顯示的新標題，寫在標題案例中。 |
| `xdm:description` | 可新增選用說明及標題。 |
| `meta:enum` | 如果以指示的欄位 `xdm:sourceProperty` 是字串欄位， `meta:enum` 可用來為區段UI中的欄位新增建議值。 請務必注意 `meta:enum` 不會宣告分項或提供XDM欄位的任何資料驗證。<br><br>此欄位僅應用於Adobe定義的核心XDM欄位。 如果來源屬性是貴組織定義的自訂欄位，您應改為編輯欄位的 `meta:enum` 屬性，直接透過欄位的上層資源的PATCH請求。 |
| `meta:excludeMetaEnum` | 如果以指示的欄位 `xdm:sourceProperty` 是字串欄位，其中包含 `meta:enum` 欄位中，您可以將此物件包含在易記名稱描述元中，以從分段中排除這些值的部分或全部。 每個項目的鍵值和值必須與原始條目中包含的鍵值和值匹配 `meta:enum` ，以便排除項目。 |

{style=&quot;table-layout:auto&quot;}

#### 關係描述符

關係描述符描述了兩個不同架構之間的關係，它們以下中所述的屬性為基礎 `sourceProperty` 和 `destinationProperty`. 請參閱 [定義兩個結構之間的關係](../tutorials/relationship-api.md) 以取得更多資訊。

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
| `@type` | 要定義的描述符的類型。 對於關係描述符，此值必須設定為 `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | 此 `$id` 定義描述符的架構的URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 定義關係的源架構中欄位的路徑。 應以「/」開頭，而非以「/」結尾。 請勿在路徑中包含「properties」（例如「/personalEmail/address」，而非「/properties/personalEmail/properties/address」）。 |
| `xdm:destinationSchema` | 此 `$id` 此描述符正在定義與的關係的目標架構的URI。 |
| `xdm:destinationVersion` | 目標架構的主要版本。 |
| `xdm:destinationProperty` | 目標架構內目標欄位的可選路徑。 如果省略此屬性，則目標欄位將由包含匹配引用標識描述符的任何欄位推斷（請參見下面）。 |

{style=&quot;table-layout:auto&quot;}

#### 引用標識描述符

參考身份描述符提供指向架構欄位主要身份的參考上下文，允許其他架構中的欄位引用它。 目標架構必須已定義主標識欄位，然後才能通過此描述符由其他架構引用。

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
| `@type` | 要定義的描述符的類型。 對於引用標識描述符，此值必須設定為 `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | 此 `$id` 定義描述符的架構的URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 用於引用目標架構的源架構中欄位的路徑。 應以「/」開頭，而非以「/」結尾。 請勿在路徑中加入「屬性」(例如 `/personalEmail/address` 而非 `/properties/personalEmail/properties/address`)。 |
| `xdm:identityNamespace` | 原始碼屬性的身份命名空間代碼。 |

{style=&quot;table-layout:auto&quot;}

#### 已棄用的欄位描述符

您可以 [取代自訂XDM資源中的欄位](../tutorials/field-deprecation.md#custom) 新增 `meta:status` 屬性設定為 `deprecated` 到有關的欄位。 但是，如果您想要取代結構中標準XDM資源提供的欄位，您可以將已棄用的欄位描述元指派給相關結構，以達到相同的效果。 使用 [正確 `Accept` 標題](../tutorials/field-deprecation.md#verify-deprecation)，您就可以在API中查詢結構時，檢視哪些標準欄位已遭取代。

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
| `@type` | 描述符的類型。 對於欄位取代描述符，此值必須設定為 `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` 應用描述符的架構。 |
| `xdm:sourceVersion` | 要應用描述符的架構的版本。 應設為 `1`. |
| `xdm:sourceProperty` | 應用描述符的架構內屬性的路徑。 如果要將描述符應用於多個屬性，可以以陣列的形式提供路徑清單(例如， `["/firstName", "/lastName"]`)。 |

{style=&quot;table-layout:auto&quot;}
