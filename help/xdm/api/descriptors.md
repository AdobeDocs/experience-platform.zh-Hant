---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 描述符
topic: developer guide
translation-type: tm+mt
source-git-commit: b021b6813af18e29f544dc55541f23dd7dd57d47
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 1%

---


# 描述符

結構定義資料實體的靜態視圖，但不提供基於這些結構的資料（例如資料集）如何彼此關聯的具體詳細資訊。 Adobe Experience Platform可讓您使用描述子來描述這些關係以及關於架構的其他解釋性中繼資料。

架構描述子是租用戶層級的中繼資料，這表示它們對您的IMS組織是獨一無二的，所有描述子操作都發生在租用戶容器中。

每個模式都可以應用一個或多個模式描述符實體。 每個模式描述符實體都包 `@type` 括描述符 `sourceSchema` 及其應用對象。 應用後，這些描述符將應用於使用模式建立的所有資料集。

本文檔提供描述符的示例API調用，以及可用描述符的完整清單和定義每種類型所需的欄位。

>[!NOTE]
>
>描述符需要用唯一的「接受」標 `xed` 頭來替 `xdm`換，但其外觀與「接受」標頭在中其它位置使用非常相似 [!DNL Schema Registry]。 下列範例呼叫中已包含正確的「接受」標題，但請格外小心，以確保使用正確的標題。

## 清單描述符

單個GET請求可用於返回由您的組織定義的所有描述符的清單。

**API格式**

```http
GET /tenant/descriptors
```

**請求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

回應格式取決於請求中傳送的「接受」標題。 請注意，端 `/descriptors` 點使用與API中所有其他端點不同的「接受」 [!DNL Schema Registry] 標題。

描述符接受標 `xed` 頭替 `xdm`換為，並提供 `link` 描述符唯一的選項。

| 接受 | 說明 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID的陣列 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路徑的陣列 |
| `application/vnd.adobe.xdm+json` | 返回擴展描述符對象的陣列 |

**回應**

該響應包括用於具有已定義描述符的每個描述符類型的陣列。 換句話說，如果沒有某個定義的描述符，則 `@type` 註冊表將不返回該描述符類型的空陣列。

使用「接 `link` 受」標頭時，每個描述符都以格式顯示為陣列項 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

## 查找描述符

如果要查看特定描述符的詳細資訊，可以使用其查找(GET)單個描述符 `@id`。

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要 `@id` 查找的描述符。 |

**請求**

描述符沒有版本化，因此在查找請求中不需要「接受」標頭。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回描述符的詳細資訊，包括其 `@type` 和 `sourceSchema`，以及根據描述符類型而不同的其他資訊。 傳回的 `@id` 描述符應與請求中 `@id` 提供的描述符相符。

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

## 建立描述符

允許 [!DNL Schema Registry] 您定義幾種不同的描述符類型。 每個描述符類型都需要在POST請求中發送其自己的特定欄位。 定義描述符的附錄部分提供了描述符的完整清單以及定義它們所需 [的欄位](#defining-descriptors)。

**API格式**

```http
POST /tenant/descriptors
```

**請求**

以下請求在示例方案的「電子郵件地址」欄位上定義身份描述符。 這會告 [!DNL Experience Platform] 訴您使用電子郵件地址做為識別碼，以協助拼湊個人的相關資訊。

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

成功的響應返回HTTP狀態201（已建立）和新建立的描述符的詳細資訊，包括其詳細資訊 `@id`。 是 `@id` 由指派的只讀欄位，用 [!DNL Schema Registry] 於引用API中的描述符。

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

## 更新描述符

通過使PUT請求引用要在請求路徑中更 `@id` 新的描述符，可以更新描述符。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要 `@id` 更新的描述符。 |

**請求**

此請求基 _本上重寫描述符_ ，因此請求主體必須包含定義該類型描述符所需的所有欄位。 換言之，要更新(PUT)描述符的請求裝載與要建立(POST)相同類型描述符的裝載相同。

在此範例中，身分描述子正在更新，以參考不 `xdm:sourceProperty` 同（「行動電話」），並將 `xdm:namespace` 變更為「Phone」。

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

有關屬性和 `xdm:namespace` 的詳 `xdm:property`細資訊，包括如何訪問這些屬性，請參閱定義描述符的附 [錄部分](#defining-descriptors)。

**回應**

成功的回應會傳回HTTP狀態201（已建立）和 `@id` 更新描述符的狀態(應符合請 `@id` 求中傳送的描述符)。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

執行查閱(GET)請求以查看描述符時，將顯示欄位現在已更新，以反映在PUT請求中發送的更改。

## 刪除描述符

有時，您可能需要刪除已從中定義的描述符 [!DNL Schema Registry]。 通過引用要刪除的描述符的DELETE `@id` 請求來完成此操作。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要 `@id` 刪除的描述符。 |

**請求**

刪除描述符時不需要接受標頭。

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

要確認描述符已刪除，可以對描述符執行查找請求 `@id`。 響應返回HTTP狀態404（找不到），因為描述符已從中刪除 [!DNL Schema Registry]。

## 附錄

下節提供了有關在 [!DNL Schema Registry] API中使用描述符的其他資訊。

### 定義描述符

以下各節概述了可用描述符類型，包括定義每種類型描述符的必需欄位。

#### 身份描述符

身分描述符表示&quot;[!UICONTROL sourceSchema]&quot;的&quot;sourceProperty[!UICONTROL &quot;是]Adobe Experience Platform Identity Service所述的 [!DNL Identity] 欄位 [](../../identity-service/home.md)。

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
| `xdm:sourceSchema` | 定義 `$id` 描述符的方案的URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 將作為身份的特定屬性的路徑。 路徑應以&quot;/&quot;開頭，而不以&quot;/&quot;結束。 路徑中不包含「屬性」（例如，使用「/personalEmail/address」而非「/properties/personalEmail/properties/address」） |
| `xdm:namespace` | 身 `id` 分名 `code` 稱空間的或值。 使用可找到名稱空間清單 [!DNL Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)。 |
| `xdm:property` | 或 `xdm:id` , `xdm:code`視使用者 `xdm:namespace` 而定。 |
| `xdm:isPrimary` | 選用的布林值。 若為true，則將欄位指示為主要身分。 結構只能包含一個主要標識。 |

#### 友好名稱描述符

好記的名稱描述符允許用戶修改 `title`核心庫 `description`模式 `meta:enum` 欄位的、和值。 當使用您想要標示為包含您組織特定資訊的「eVar」和其他「一般」欄位時，特別有用。 UI可使用這些來顯示更好記的名稱，或僅顯示具有好記名稱的欄位。

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
| `xdm:sourceSchema` | 定義 `$id` 描述符的方案的URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 將作為身份的特定屬性的路徑。 路徑應以&quot;/&quot;開頭，而不以&quot;/&quot;結束。 路徑中不包含「屬性」（例如，使用「/personalEmail/address」而非「/properties/personalEmail/properties/address」） |
| `xdm:title` | 您要為此欄位顯示的新標題，在「標題大小寫」中撰寫。 |
| `xdm:description` | 可隨標題新增選擇性說明。 |
| `meta:enum` | 如果由指示的欄 `xdm:sourceProperty` 位是字串欄位， `meta:enum` 會決定UI中欄位的建議值 [!DNL Experience Platform] 清單。 請務必注意，不 `meta:enum` 要聲明枚舉或為XDM欄位提供任何資料驗證。<br><br>這僅應用於Adobe定義的核心XDM欄位。 如果來源屬性是您組織定義的自訂欄位，您應直接透過 `meta:enum` PATCH請求編輯欄位 [屬性](./update-resource.md)。 |

#### 關係描述子

關係描述符描述了兩個不同模式之間的關係，它們基於和中描述的屬 `sourceProperty` 性鍵 `destinationProperty`入。 如需詳細資訊，請 [參閱定義兩個結構之間的關係](../tutorials/relationship-api.md) 的教學課程。

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
| `xdm:sourceSchema` | 定義 `$id` 描述符的方案的URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 定義關係的源架構中欄位的路徑。 應以&quot;/&quot;開頭，而非以&quot;/&quot;結尾。 不要在路徑中包含「屬性」（例如，「/personalEmail/address」，而不是「/properties/personalEmail/properties/address」）。 |
| `xdm:destinationSchema` | 此描 `$id` 述符正在定義與的關係的目標模式的URI。 |
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
| `xdm:sourceSchema` | 定義 `$id` 描述符的方案的URI。 |
| `xdm:sourceVersion` | 源架構的主要版本。 |
| `xdm:sourceProperty` | 定義描述符的源模式中欄位的路徑。 應以&quot;/&quot;開頭，而非以&quot;/&quot;結尾。 不要在路徑中包含「屬性」（例如，「/personalEmail/address」，而不是「/properties/personalEmail/properties/address」）。 |
| `xdm:identityNamespace` | source屬性的識別名稱空間代碼。 |