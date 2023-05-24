---
solution: Experience Platform
title: 在UI中導出XDM架構
description: 瞭解如何將現有架構導出到Adobe Experience Platform用戶介面中的其他沙箱或組織。
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: bed627b945c5392858bcc2dce18e9bbabe8bcdb6
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# 在UI中導出XDM架構

架構庫中的所有資源都包含在組織內的特定沙箱中。 在某些情況下，您可能希望在沙箱和組織之間共用經驗資料模型(XDM)資源。

為滿足此需求， [!UICONTROL 架構] 使用Adobe Experience PlatformUI中的工作區，可以為架構庫中的任何架構生成導出負載。 然後，此負載可用於調用架構註冊表API，以將架構（和所有從屬資源）導入目標沙箱和組織中。

>[!NOTE]
>
>您還可以使用方案註冊表API導出除方案外的其他資源，包括類、方案欄位組和資料類型。 查看 [導出終結點指南](../api/export.md) 的子菜單。

## 先決條件

雖然平台UI允許導出XDM資源，但必須使用架構註冊表API將這些資源導入其他沙箱或組織以完成工作流。 請參閱上的指南 [架構註冊表API入門](../api/getting-started.md) 有關本指南之前所需的身份驗證標頭的重要資訊。

## 生成導出負載 {#generate-export-payload}

在平台UI中，選擇 **[!UICONTROL 架構]** 的子菜單。 在 [!UICONTROL 架構] 工作區，選擇要導出的架構的行以在右側欄中顯示架構詳細資訊。

>[!TIP]
>
>請參閱上的指南 [探索XDM資源](./explore.md) 有關如何查找要查找的XDM資源的詳細資訊。

接下來，選擇 **[!UICONTROL 複製JSON]** 表徵圖。![複製表徵圖](../images/ui/export/icon.png))。

![具有架構行和 [!UICONTROL 複製到JSON] 。](../images/ui/export/copy-json.png)

這會將JSON負載複製到剪貼簿，並基於架構結構生成。 對於「」[!DNL Loyalty Members]&quot;上面所示的架構，將生成以下JSON:

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty details",
    "type": "object",
    "description": "",
    "definitions": {
      "customFields": {
        "type": "object",
        "properties": {
          "_<XDM_TENANTID_PLACEHOLDER>": {
            "type": "object",
            "properties": {
              "loyalty": {
                "title": "Loyalty",
                "description": "",
                "type": "object",
                "isRequired": false,
                "required": [
                  
                ],
                "properties": {
                  "loyaltyId": {
                    "title": "Loyalty ID",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "string"
                  },
                  "memberSince": {
                    "title": "Member Since",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "format": "date",
                    "meta:xdmType": "date"
                  },
                  "points": {
                    "title": "Points",
                    "description": "",
                    "type": "integer",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "int"
                  },
                  "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "enum": [
                      "platinum",
                      "gold",
                      "silver",
                      "bronze"
                    ],
                    "meta:enum": {
                      "platinum": "Platinum",
                      "gold": "Gold",
                      "silver": "Silver",
                      "bronze": "Bronze"
                    },
                    "meta:xdmType": "string"
                  }
                },
                "meta:xdmType": "object"
              }
            },
            "meta:xdmType": "object"
          }
        },
        "meta:xdmType": "object"
      }
    },
    "allOf": [
      {
        "$ref": "#/definitions/customFields",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
      
    ],
    "meta:xdmType": "object",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production"
  },
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/schemas/1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.schemas.1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Describes customers who are members of a loyalty program.",
    "allOf": [
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/mixins/profile-consents",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
      "https://ns.adobe.com/xdm/context/profile-person-details",
      "https://ns.adobe.com/xdm/context/profile-personal-details",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile",
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/mixins/profile-consents"
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production",
    "meta:immutableTags": [
      
    ]
  }
]
```

負載採用陣列的形式，每個陣列項都是表示要導出的自定義XDM資源的對象。 在上例中， &quot;[!DNL Loyalty details]&quot;自定義欄位組和&quot;[!DNL Loyalty Members]&quot;架構。 導出中不包含模式使用的任何核心資源，因為這些資源在所有沙箱和組織中都可用。

請注意，您組織的租戶ID的每個實例都顯示為 `<XDM_TENANTID_PLACEHOLDER>` 在有效載荷中。 這些佔位符將自動替換為相應的租戶ID值，具體取決於您在下一步中導入架構的位置。

## 使用API導入資源

複製架構的導出JSON後，可以將其用作POST請求的負載 `/rpc/import` 架構註冊表API中的終結點。 查看 [導入終結點指南](../api/import.md) 有關如何配置調用以將架構發送到所需組織和沙盒的詳細資訊。

## 後續步驟

按照本指南，您已成功將XDM架構導出到其他組織或沙盒。 有關功能的詳細資訊 [!UICONTROL 架構] UI，請參閱 [[!UICONTROL 架構] UI概述](./overview.md)。
