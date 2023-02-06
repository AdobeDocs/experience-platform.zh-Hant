---
title: 管理API中的建議值
description: 了解如何將建議的值新增至Schema Registry API中的字串欄位。
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 管理API中的建議值

對於Experience Data Model(XDM)中的任何字串欄位，您可以定義 **列舉** 將欄位可內嵌的值限制為預先定義的集。 如果您嘗試將資料內嵌至列舉欄位，而值不符合其設定中定義的任何欄位，則擷取將會遭到拒絕。

與列舉不同，請新增 **建議值** 字串欄位的值不會限制可擷取的值。 反之，建議的值會影響 [區段UI](../../segmentation/ui/overview.md) 將字串欄位納入為屬性時。

>[!NOTE]
>
>欄位的更新建議值會延遲約五分鐘，以反映在分段UI中。

本指南說明如何使用 [結構註冊表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 如需如何在Adobe Experience Platform使用者介面中執行此動作的步驟，請參閱 [列舉和建議值的UI指南](../ui/fields/enum.md).

## 先決條件

本指南假設您熟悉XDM中架構組成的元素，以及如何使用Schema Registry API來建立和編輯XDM資源。 如需簡介，請參閱下列檔案：

* [結構構成基本概念](../schema/composition.md)
* [Schema Registry API指南](../api/overview.md)

強烈建議您檢閱 [列舉和建議值的演化規則](../ui/fields/enum.md#evolution) 如果要更新現有欄位。 如果您要管理參與聯合的結構的建議值，請參閱 [合併列舉和建議值的規則](../ui/fields/enum.md#merging).

## 組合物

在API中， **列舉** 欄位由 `enum` 陣列，若 `meta:enum` 物件提供這些值的好記顯示名稱：

```json
"exampleStringField": {
  "type": "string",
  "enum": [
    "value1",
    "value2",
    "value3"
  ],
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

對於枚舉欄位，架構註冊表不允許 `meta:enum` 將擴展到 `enum`，因為嘗試擷取這些限制以外的字串值時，無法通過驗證。

或者，您可以定義不包含 `enum` 陣列，且僅使用 `meta:enum` 物體表示 **建議值**:

```json
"exampleStringField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

因為字串沒有 `enum` 陣列來定義約束，其 `meta:enum` 屬性可延伸以包含新值。

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## 將建議的值新增至標準欄位 {#add-suggested-standard}

若要擴充 `meta:enum` ，您可以建立 [友好名稱描述符](../api/descriptors.md#friendly-name) 針對特定結構中的相關欄位。

>[!NOTE]
>
>字串欄位的建議值只能在架構層級新增。 換句話說，將 `meta:enum` 標準欄位的其他結構不會影響採用相同標準欄位的其他結構。

下列請求會將建議的值新增至標準 `eventType` 欄位(由 [XDM ExperienceEvent類別](../classes/experienceevent.md))，適用於 `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "sourceProperty": "/eventType",
        "title": {
            "en_us": "Enum Event Type"
        },
        "description": {
            "en_us": "Event type field with soft enum values"
        },
        "meta:enum": {
          "eventA": {
            "en_us": "Event Type A"
          },
          "eventB": {
            "en_us": "Event Type B"
          }
        }
      }'
```

應用描述符後，當檢索架構時，架構註冊表使用以下內容進行響應（響應因空間而截斷）:

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "eventType": {
      "type":"string",
      "title": "Enum Event Type",
      "description": "Event type field with soft enum values.",
      "meta:enum": {
        "customEventA": "Custom Event Type A",
        "customEventB": "Custom Event Type B"
      }
    }
  }
}
```

>[!NOTE]
>
>如果標準欄位已包含 `meta:enum`，則描述符的新值不會覆寫現有欄位，而會改為在上新增：
>
>
```json
>"standardField": {
>   "type":"string",
>   "title": "Example standard enum field",
>   "description": "Standard field with existing enum values.",
>   "meta:enum": {
>       "standardEventA": "Standard Event Type A",
>       "standardEventB": "Standard Event Type B",
>       "customEventA": "Custom Event Type A",
>       "customEventB": "Custom Event Type B"
>   }
>}
>```

<!-- ### Remove suggested values {#remove-suggested-standard}

If a standard string field has predefined suggested values, you can remove any values that you do not wish to see in segmentation. This is done through by creating a [friendly name descriptor](../api/descriptors.md#friendly-name) for the schema that includes an `xdm:excludeMetaEnum` property.

**API format**

```http
POST /tenant/descriptors
```

**Request**

The following request removes the suggested values "[!DNL Web Form Filled Out]" and "[!DNL Media ping]" for `eventType` in a schema based on the [XDM ExperienceEvent class](../classes/experienceevent.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/xdm:eventType",
        "xdm:excludeMetaEnum": {
          "web.formFilledOut": "Web Form Filled Out",
          "media.ping": "Media ping"
        }
      }'
```

| Property | Description |
| --- | --- |
| `@type` | The type of descriptor being defined. For a friendly name descriptor, this value must be set to `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI of the schema where the descriptor is being defined. |
| `xdm:sourceVersion` | The major version of the source schema. |
| `xdm:sourceProperty` | The path to the specific property whose suggested values you want to manage. The path should begin with a slash (`/`) and not end with one. Do not include `properties` in the path (for example, use `/personalEmail/address` instead of `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | An object that describes the suggested values that should be excluded for the field in segmentation. The key and value for each entry must match those included in the original `meta:enum` of the field in order for the entry to be excluded.  |

{style="table-layout:auto"}

**Response**

A successful response returns HTTP status 201 (Created) and the details of the newly created descriptor. The suggested values included under `xdm:excludeMetaEnum` will now be hidden from the Segmentation UI.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out"
  },
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
``` -->

## 管理自訂欄位的建議值 {#suggested-custom}

若要管理 `meta:enum` 在自訂欄位中，您可以透過PATCH請求更新欄位的上層類別、欄位群組或資料類型。

>[!WARNING]
>
>與標準欄位相反，請更新 `meta:enum` 自訂欄位的其他結構會影響使用該欄位的所有結構。 如果您不想讓變更傳播至不同結構，請考慮改為建立新的自訂資源：
>
>* [建立自訂類別](../api/classes.md#create)
>* [建立自訂欄位群組](../api/field-groups.md#create)
>* [建立自訂資料類型](../api/data-types.md#create)


下列請求會更新 `meta:enum` 自訂資料類型提供的「忠誠度等級」欄位中：

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/loyaltyLevel/meta:enum",
          "value": {
            "ultra-platinum": "Ultra Platinum",
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          }
        }
      ]'
```

應用更改後，當檢索架構時，架構註冊表將使用以下內容進行響應（響應因空間而截斷）:

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "loyaltyLevel": {
      "type":"string",
      "title": "Loyalty Level",
      "description": "The loyalty program tier that this customer qualifies for.",
      "meta:enum": {
        "ultra-platinum": "Ultra Platinum",
        "platinum": "Platinum",
        "gold": "Gold",
        "silver": "Silver",
        "bronze": "Bronze"
      }
    }
  }
}
```

## 後續步驟

本指南說明如何管理Schema Registry API中字串欄位的建議值。 請參閱 [定義API中的自訂欄位](./custom-fields-api.md) ，以了解如何建立不同欄位類型的詳細資訊。
