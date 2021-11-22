---
title: 擴展軟枚舉欄位
description: 了解如何擴充Schema Registry API中的軟列舉欄位。
source-git-commit: 2d85db789e6e6a28402bb68122a3b5cfe9d0c5dc
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# 擴充軟列舉欄位

在Experience Data Model(XDM)中，列舉欄位代表字串欄位，其受限於預先定義的值子集。 列舉欄位可提供驗證，以確保擷取的資料符合一組接受的值（稱為「硬列舉」），或者它們只能表示一組建議的值，而不強制執行限制（稱為「軟列舉」）。

在結構註冊表API中，硬列舉的限制值由 `enum` 陣列，若 `meta:enum` 物件提供這些值的好記顯示名稱：

```json
"sampleHardEnumField": {
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

對於硬列舉欄位，架構註冊表不允許 `meta:enum` 將擴展到 `enum`，因為嘗試擷取這些限制以外的字串值時，無法通過驗證。

相較之下，軟列舉欄位不包含 `enum` 陣列，且僅使用 `meta:enum` 物件，表示建議的值：

```json
"sampleSoftEnumField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

由於軟列舉與硬列舉的驗證限制不同，因此其 `meta:enum` 屬性可延伸以包含新值。 本教學課程涵蓋如何擴充Schema Registry API中的標準和自訂軟式列舉欄位。

## 先決條件

本指南假設您熟悉XDM中架構組成的元素，以及如何使用Schema Registry API來建立和編輯XDM資源。 如需簡介，請參閱下列檔案：

* [結構構成基本概念](../schema/composition.md)
* [Schema Registry API指南](../api/overview.md)

## 擴充標準軟列舉欄位

若要擴充 `meta:enum` ，您可以建立 [友好名稱描述符](../api/descriptors.md#friendly-name) 針對特定結構中的相關欄位。

>[!NOTE]
>
>標準軟列舉只能在架構層級擴充。 換句話說，將 `meta:enum` 標準欄位的其他結構不會影響採用相同標準欄位的其他結構。

下列請求會將軟列舉值新增至標準 `eventType` 欄位(由 [XDM ExperienceEvent類別](../classes/experienceevent.md))，適用於 `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## 擴充自訂軟列舉欄位

若要擴充 `meta:enum` 在自訂欄位中，您可以透過PATCH請求更新欄位的上層類別、欄位群組或資料類型。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

本指南說明如何擴充Schema Registry API中的軟列舉。 如需如何在API中定義不同欄位類型的詳細資訊，請參閱 [XDM欄位類型限制](../schema/field-constraints.md#define-fields).
