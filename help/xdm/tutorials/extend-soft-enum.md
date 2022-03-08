---
title: 擴展軟枚舉欄位
description: 瞭解如何在架構註冊表API中擴展軟枚舉欄位。
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a26c8d43ff7874bcedd2adb3d6da995986198c96
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 擴展軟枚舉欄位

在體驗資料模型(XDM)中，枚舉欄位表示一個字串欄位，該字串欄位被限制為預定義的值子集。 枚舉欄位可以提供驗證以確保所攝取的資料符合一組接受的值（稱為「硬枚舉」），或者它們只能表示一組建議的值而不強制約束（稱為「軟枚舉」）。

在架構註冊表API中，硬枚舉的約束值由 `enum` 陣列，而 `meta:enum` object為這些值提供友好的顯示名稱：

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

對於硬枚舉欄位，架構註冊表不允許 `meta:enum` 將擴展到下面提供的值之外 `enum`，因為嘗試在這些約束之外輸入字串值將不會通過驗證。

相反，軟枚舉欄位不包含 `enum` 僅使用 `meta:enum` 對象表示建議的值：

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

由於軟枚舉與硬枚舉的驗證約束不相同，因此它們 `meta:enum` 可以擴展屬性以包括新值。 本教程介紹如何擴展架構註冊表API中的標準和自定義可變枚舉欄位。

## 先決條件

本指南假定您熟悉XDM中模式組合的元素以及如何使用模式註冊表API建立和編輯XDM資源。 如需介紹，請參閱以下文檔：

* [架構組合的基礎](../schema/composition.md)
* [架構註冊API指南](../api/overview.md)

## 擴展標準軟枚舉欄位

擴展 `meta:enum` 在標準字串欄位中，可以建立 [友好名稱描述符](../api/descriptors.md#friendly-name) 的子菜單。

>[!NOTE]
>
>只能在架構級別擴展標準軟枚舉。 換句話說， `meta:enum` 模式中的標準欄位不會影響使用相同標準欄位的其他模式。

以下請求將可變枚舉值添加到標準 `eventType` 欄位(由 [XDM ExperienceEvent類](../classes/experienceevent.md))，用於在 `sourceSchema`:

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

應用描述符後，在檢索架構時，架構註冊表會以下方式作出響應（因空間而截斷的響應）:

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
>如果標準欄位已包含以下值 `meta:enum`，描述符中的新值不會覆蓋現有欄位，而是添加到：
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

## 擴展自定義軟枚舉欄位

擴展 `meta:enum` 在自定義欄位中，您可以通過PATCH請求更新欄位的父類、欄位組或資料類型。

>[!WARNING]
>
>與標準欄位不同，更新 `meta:enum` 自定義欄位會影響使用該欄位的所有其他架構。 如果不希望更改在方案間傳播，請考慮改為建立新的自定義資源：
>
>* [建立自定義類](../api/classes.md#create)
>* [建立自定義欄位組](../api/field-groups.md#create)
>* [建立自定義資料類型](../api/data-types.md#create)


以下請求更新 `meta:enum` 自定義資料類型提供的「忠誠度級別」欄位：

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

應用更改後，在檢索架構時，架構註冊表會以下方式作出響應（因空間而截斷的響應）:

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

本指南介紹如何擴展架構註冊表API中的軟枚舉。 請參閱上的指南 [定義API中的自定義欄位](./custom-fields-api.md) 的子菜單。
