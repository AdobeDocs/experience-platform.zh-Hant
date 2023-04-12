---
solution: Experience Platform
title: 在UI中匯出XDM結構
description: 了解如何在Adobe Experience Platform使用者介面中，將現有結構匯出至不同的沙箱或組織。
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# 在UI中匯出XDM結構

結構資料庫中的所有資源都包含在組織內的特定沙箱中。 在某些情況下，您可能會想在沙箱和組織之間共用Experience Data Model(XDM)資源。

為滿足此需求， [!UICONTROL 結構] Adobe Experience Platform UI中的工作區可讓您為架構資料庫中的任何架構產生匯出裝載。 然後，此裝載可用於呼叫Schema Registry API，以將結構（以及所有相依資源）匯入目標沙箱和組織中。

>[!NOTE]
>
>除了結構（包括類、結構欄位組和資料類型）外，您還可以使用結構註冊表API導出其他資源。 請參閱 [匯出端點指南](../api/export.md) 以取得更多資訊。

## 先決條件

雖然Platform UI可讓您匯出XDM資源，但您必須使用Schema Registry API將這些資源匯入其他沙箱或組織，才能完成工作流程。 請參閱 [架構註冊表API快速入門](../api/getting-started.md) 如需遵循本指南之前所需驗證標題的重要資訊。

## 產生匯出裝載

在平台UI中，選取 **[!UICONTROL 結構]** 的下一頁。 在 [!UICONTROL 結構] 工作區，找出您要匯出的結構，並在 [!DNL Schema Editor].

>[!TIP]
>
>請參閱 [探索XDM資源](./explore.md) 以取得如何尋找您所尋找之XDM資源的詳細資訊。

開啟架構後，請選取 **[!UICONTROL 複製JSON]** 圖示(![復製圖示](../images/ui/export/icon.png))。

![](../images/ui/export/copy-json.png)

這會根據結構，將JSON裝載複製到剪貼簿。 針對「[!DNL Loyalty Members]&quot;結構（如上所示）會產生下列JSON:

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

裝載會以陣列的形式呈現，而每個陣列項目都是代表要匯出之自訂XDM資源的物件。 在上例中，[!DNL Loyalty details]&quot;自定義欄位組和&quot;[!DNL Loyalty Members]」架構。 匯出中不會包含架構使用的任何核心資源，因為這些資源可用於所有沙箱和組織。

請注意，您組織的租用戶ID的每個例項都顯示為 `<XDM_TENANTID_PLACEHOLDER>` 在裝載中。 視您在下個步驟中匯入結構的位置而定，這些預留位置會自動取代為適當的租用戶ID值。

## 使用API匯入資源

複製結構的匯出JSON後，您就可以將它當作POST要求的裝載，傳送至 `/rpc/import` 結構註冊表API中的端點。 請參閱 [匯入端點指南](../api/import.md) 如需如何設定呼叫以將結構傳送至所需組織和沙箱的詳細資訊。

## 後續步驟

依照本指南，您已成功將XDM結構匯出至不同的組織或沙箱。 如需功能的詳細資訊，請參閱 [!UICONTROL 結構] UI，請參閱 [[!UICONTROL 結構] UI概述](./overview.md).
