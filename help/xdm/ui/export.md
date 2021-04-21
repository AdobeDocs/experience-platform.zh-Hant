---
solution: Experience Platform
title: 在UI中匯出XDM結構描述
description: 瞭解如何在Adobe Experience Platform使用者介面中將現有的架構匯出至不同的沙盒或IMS組織。
topic-legacy: user guide
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# 在UI中匯出XDM結構

架構程式庫中的所有資源都包含在IMS組織內的特定沙盒中。 在某些情況下，您可能會想在沙盒和IMS組織之間共用「體驗資料模型」(XDM)資源。

為滿足此需求，Adobe Experience PlatformUI中的[!UICONTROL Schemas]工作區允許您為架構庫中的任何架構生成導出裝載。 然後，此裝載可用於對架構註冊表API的呼叫，以將架構（及所有相依資源）匯入目標沙盒和IMS組織。

>[!NOTE]
>
>您也可以使用「方案註冊表API」來匯出其他資源，以及方案，包括類別、混合和資料類型。 如需詳細資訊，請參閱[匯出／匯入端點](../api/export-import.md)上的指南。

## 先決條件

雖然平台UI可讓您匯出XDM資源，但您必須使用架構註冊表API將這些資源匯入其他沙盒或IMS組織，以完成工作流程。 在遵循本指南之前，請參閱[快速入門手冊中的「架構註冊表API](../api/getting-started.md)」，以取得有關必要驗證標題的重要資訊。

## 產生匯出裝載

在平台UI中，選擇左側導覽中的&#x200B;**[!UICONTROL Schemas]**。 在[!UICONTROL Schemas]工作區中，找到要導出的方案，並在[!DNL Schema Editor]中將其開啟。

>[!TIP]
>
>有關如何查找所查找的XDM資源的詳細資訊，請參見[中的指南。](./explore.md)

在模式開啟後，選擇畫布右上角的&#x200B;**[!UICONTROL Copy JSON]**&#x200B;表徵圖（![複製表徵圖](../images/ui/export/icon.png)）。

![](../images/ui/export/copy-json.png)

這會將JSON裝載複製至您的剪貼簿，並根據結構產生。 對於上述的&quot;[!DNL Loyalty Members]&quot;結構，會產生下列JSON:

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

裝載採用陣列的形式，每個陣列項都是表示要導出的自定義XDM資源的對象。 在上述範例中，「[!DNL Loyalty details]」自訂混音和「[!DNL Loyalty Members]」結構包含在內。 匯出中不會包含架構採用的任何核心資源，因為這些資源可用於所有沙盒和IMS組織。

請注意，您組織的租用戶ID的每個例項在裝載中會顯示為`<XDM_TENANTID_PLACEHOLDER>`。 這些預留位置會自動取代為適當的租用戶ID值，這取決於您在下一步驟中匯入架構的位置。

## 使用API匯入資源

在您複製結構的匯出JSON後，就可將它當做結構註冊表API中`/import`端點的POST要求的裝載。 如需如何設定呼叫，將結構傳送至所需IMS組織與沙盒的詳細資訊，請參閱API](../api/export-import.md#import)中有關匯入XDM資源的章節。[

## 後續步驟

依照本指南，您已成功將XDM架構匯出至不同的IMS組織或沙盒。 有關[!UICONTROL Schemas] UI功能的詳細資訊，請參閱[[!UICONTROL Schemas] UI概述](./overview.md)。
