---
keywords: Experience Platform；主題；熱門主題；api;XDM;XDM;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；架構註冊；模式註冊；描述符；描述符；描述符；描述符；標識；身份；友好名稱；替代顯示資訊；參考；關係；關係
solution: Experience Platform
title: 描述符API終結點
description: 通過架構註冊表API中的/descriptors終結點，可以以寫程式方式管理體驗應用程式中的XDM描述符。
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1872'
ht-degree: 1%

---

# 描述符終結點

方案定義資料實體的靜態視圖，但不提供關於基於這些方案（例如資料集）的資料如何彼此關聯的特定詳細資訊。 Adobe Experience Platform允許您使用描述符描述這些關係和關於架構的其他解釋性元資料。

架構描述符是租戶級元資料，這意味著它們對您的組織是唯一的，所有描述符操作都在租戶容器中進行。

每個架構可以應用一個或多個架構描述符實體。 每個模式描述符實體包括描述符 `@type` 和 `sourceSchema` 適用的。 應用後，這些描述符將應用於使用架構建立的所有資料集。

的 `/descriptors` 端點 [!DNL Schema Registry] API允許您以寫程式方式管理體驗應用程式中的描述符。

## 快速入門

本指南中使用的端點是 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 檢索描述符清單 {#list}

通過向組織發出GET請求，可以列出組織定義的所有描述符 `/tenant/descriptors`。

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

響應格式取決於 `Accept` 請求中發送的標頭。 請注意 `/descriptors` 終結點使用 `Accept` 與所有其他端點不同的標題 [!DNL Schema Registry] API。

>[!IMPORTANT]
>
>描述符需要唯一 `Accept` 替換的標題 `xed` 與 `xdm`，並提供 `link` 描述符唯一的選項。 本 `Accept` 標頭已包括在下面的示例調用中，但要確保在使用描述符時使用正確的標頭，請格外小心。

| `Accept` 標題 | 說明 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID陣列 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路徑陣列 |
| `application/vnd.adobe.xdm+json` | 返回擴展描述符對象的陣列 |
| `application/vnd.adobe.xdm-v2+json` | 此 `Accept` 必須使用報頭才能利用分頁功能。 |

{style="table-layout:auto"}

**回應**

響應包括每個具有定義描述符的描述符類型的陣列。 換句話說，如果沒有 `@type` 定義時，註冊表將不會為該描述符類型返回空陣列。

使用 `link` `Accept` 標題，每個描述符以格式顯示為陣列項 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

如果要查看特定描述符的詳細資訊，可使用其查找(GET)單個描述符 `@id`。

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 的 `@id` 描述子的。 |

{style="table-layout:auto"}

**要求**

以下請求通過其檢索描述符 `@id` 值。 描述符未版本化，因此沒有 `Accept` 查找請求中需要標頭。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回描述符的詳細資訊，包括其 `@type` 和 `sourceSchema`，以及根據描述符類型而不同的其他資訊。 返回 `@id` 應與描述符匹配 `@id` 請求中提供。

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

通過向POST請求，可以建立新描述符 `/tenant/descriptors` 端點。

>[!IMPORTANT]
>
>的 [!DNL Schema Registry] 允許您定義多種不同的描述符類型。 每個描述符類型都要求在請求正文中發送其自己的特定欄位。 查看 [附錄](#defining-descriptors) 的子菜單。

**API格式**

```http
POST /tenant/descriptors
```

**要求**

以下請求在示例架構的「電子郵件地址」欄位上定義標識描述符。 這說明 [!DNL Experience Platform] 將電子郵件地址用作標識符，以幫助拼湊有關個人的資訊。

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

成功的響應返回HTTP狀態201（已建立）以及新建立的描述符的詳細資訊，包括其 `@id`。 的 `@id` 是由 [!DNL Schema Registry] 用於引用API中的描述符。

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

可以通過包含描述符 `@id` 的子菜單。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 的 `@id` 要更新的描述符。 |

{style="table-layout:auto"}

**要求**

此請求實質上重寫描述符，因此請求正文必須包含定義該類型的描述符所需的所有欄位。 換句話說，用於更新(PUT)描述符的請求負載與要更新的負載相同 [建立(POST)描述符](#create) 類型相同。

>[!IMPORTANT]
>
>與使用POST請求建立描述符一樣，每個描述符類型都要求在PUT請求負載中發送其自己的特定欄位。 查看 [附錄](#defining-descriptors) 的子菜單。

以下示例更新標識描述符以引用其他 `xdm:sourceProperty` (`mobile phone`)並更改 `xdm:namespace` 至 `Phone`。

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

成功的響應返回HTTP狀態201（已建立）和 `@id` 更新的描述符(應與 `@id` 請求中發送)。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

執行 [查找(GET)請求](#lookup) 要查看描述符，將顯示欄位現在已更新以反映在PUT請求中發送的更改。

## 刪除描述符 {#delete}

有時，您可能需要刪除從 [!DNL Schema Registry]。 這是通過發出引用 `@id` 刪除的描述符。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 的 `@id` 刪除的描述符。 |

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

成功的響應返回HTTP狀態204（無內容）和空白正文。

要確認描述符已被刪除，可以執行 [查找請求](#lookup) 描述符 `@id`。 響應返回HTTP狀態404（未找到），因為描述符已從 [!DNL Schema Registry]。

## 附錄

以下部分提供了有關使用中的描述符的其他資訊 [!DNL Schema Registry] API。

### 定義描述符 {#defining-descriptors}

以下各節概述了可用的描述符類型，包括定義每種類型的描述符的必需欄位。

#### 標識描述符

標識描述符表示[!UICONTROL sourceProperty]「 」[!UICONTROL 源架構]「是 [!DNL Identity] 欄位，如所述 [Adobe Experience Platform身份服務](../../identity-service/home.md)。

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
| `@type` | 正在定義的描述符的類型。 對於標識描述符，必須將此值設定為 `xdm:descriptorIdentity`。 |
| `xdm:sourceSchema` | 的 `$id` 定義描述符的架構的URI。 |
| `xdm:sourceVersion` | 源架構的主版本。 |
| `xdm:sourceProperty` | 將作為標識的特定屬性的路徑。 路徑應以「/」開頭，而不以「/」結尾。 不要在路徑中包括&quot;properties&quot;（例如，使用&quot;/personalEmail/address&quot;而不是&quot;/properties/personalEmail/properties/address&quot;） |
| `xdm:namespace` | 的 `id` 或 `code` 標識名稱空間的值。 使用 [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service)。 |
| `xdm:property` | 要麼 `xdm:id` 或 `xdm:code`，具體取決於 `xdm:namespace` 。 |
| `xdm:isPrimary` | 可選布爾值。 如果為true，則將欄位指示為主標識。 架構只能包含一個主標識。 |

{style="table-layout:auto"}

#### 友好名稱描述符 {#friendly-name}

友好名稱描述符允許用戶修改 `title`。 `description`, `meta:enum` 核心庫架構欄位的值。 在使用「eVars」和其他「一般」欄位時特別有用，您希望將這些欄位標籤為包含特定於您的組織的資訊。 UI可以使用這些命令來顯示更友好的名稱或僅顯示具有友好名稱的欄位。

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
| `@type` | 正在定義的描述符的類型。 對於友好名稱描述符，必須將此值設定為 `xdm:alternateDisplayInfo`。 |
| `xdm:sourceSchema` | 的 `$id` 定義描述符的架構的URI。 |
| `xdm:sourceVersion` | 源架構的主版本。 |
| `xdm:sourceProperty` | 要修改其詳細資訊的特定屬性的路徑。路徑應以斜槓(`/`)而不是以一個結尾。 不包括 `properties` 在路徑中(例如，使用 `/personalEmail/address` 而不是 `/properties/personalEmail/properties/address`)。 |
| `xdm:title` | 要為此欄位顯示的新標題，以標題大小寫形式寫入。 |
| `xdm:description` | 可以隨標題一起添加可選說明。 |
| `meta:enum` | 如果由 `xdm:sourceProperty` 是字串欄位， `meta:enum` 可用於為「分段UI」中的欄位添加建議的值。 必須指出， `meta:enum` 不為XDM欄位聲明枚舉或提供任何資料驗證。<br><br>這隻應用於由Adobe定義的核心XDM欄位。 如果源屬性是您的組織定義的自定義欄位，則應改為編輯該欄位的 `meta:enum` 屬性直接通過PATCH請求訪問欄位的父資源。 |
| `meta:excludeMetaEnum` | 如果由 `xdm:sourceProperty` 是一個字串欄位，該欄位具有在 `meta:enum` 欄位中，可以將此對象包含在友好名稱描述符中，以從分割中排除這些值中的部分或全部。 每個條目的鍵和值必須與原始條目中包含的鍵和值匹配 `meta:enum` 的子菜單。 |

{style="table-layout:auto"}

#### 關係描述符

關係描述符描述兩個不同架構之間的關係，並對中所述的屬性進行鍵控 `sourceProperty` 和 `destinationProperty`。 請參閱上的教程 [定義兩個架構之間的關係](../tutorials/relationship-api.md) 的子菜單。

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
| `@type` | 正在定義的描述符的類型。 對於關係描述符，必須將此值設定為 `xdm:descriptorOneToOne`。 |
| `xdm:sourceSchema` | 的 `$id` 定義描述符的架構的URI。 |
| `xdm:sourceVersion` | 源架構的主版本。 |
| `xdm:sourceProperty` | 源架構中定義關係的欄位的路徑。 應以「/」開頭，而不以「/」結尾。 不要在路徑中包括「properties」（例如，「/personalEmail/address」，而不是「/properties/personalEmail/properties/address」）。 |
| `xdm:destinationSchema` | 的 `$id` 此描述符正在定義與的關係的引用架構的URI。 |
| `xdm:destinationVersion` | 引用架構的主版本。 |
| `xdm:destinationProperty` | 引用架構中目標欄位的可選路徑。 如果省略此屬性，則目標欄位將由包含匹配引用標識描述符的任何欄位來推斷（請參閱下文）。 |

{style="table-layout:auto"}

#### 引用標識描述符

引用標識描述符提供對模式欄位的主要標識的引用上下文，允許其他模式中的欄位引用它。 引用架構必須已定義一個主標識欄位，然後才能通過此描述符由其他架構引用它。

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
| `@type` | 正在定義的描述符的類型。 對於引用標識描述符，必須將此值設定為 `xdm:descriptorReferenceIdentity`。 |
| `xdm:sourceSchema` | 的 `$id` 定義描述符的架構的URI。 |
| `xdm:sourceVersion` | 源架構的主版本。 |
| `xdm:sourceProperty` | 源架構中用於引用引用架構的欄位的路徑。 應以「/」開頭，而不以「/」結尾。 路徑中不包含「屬性」(例如， `/personalEmail/address` 而不是 `/properties/personalEmail/properties/address`)。 |
| `xdm:identityNamespace` | 源屬性的標識名稱空間代碼。 |

{style="table-layout:auto"}

#### 不建議使用的欄位描述符

你可以 [棄用自定義XDM資源中的欄位](../tutorials/field-deprecation-api.md#custom) 通過添加 `meta:status` 屬性集 `deprecated` 去那個領域。 如果要棄用架構中標準XDM資源提供的欄位，則可以將已棄用的欄位描述符分配給有關的架構，以達到相同的效果。 使用 [正確 `Accept` 標題](../tutorials/field-deprecation-api.md#verify-deprecation)，然後在API中查找架構時，可以查看該架構不建議使用的標準欄位。

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
| `@type` | 描述符的類型。 對於欄位棄用描述符，必須將此值設定為 `xdm:descriptorDeprecated`。 |
| `xdm:sourceSchema` | URI `$id` 將描述符應用到的架構。 |
| `xdm:sourceVersion` | 要將描述符應用到的架構的版本。 應設定為 `1`。 |
| `xdm:sourceProperty` | 將描述符應用到的架構中的屬性的路徑。 如果要將描述符應用於多個屬性，可以以陣列的形式提供路徑清單(例如， `["/firstName", "/lastName"]`)。 |

{style="table-layout:auto"}
