---
solution: Experience Platform
title: 在UI中匯出XDM結構描述
description: 瞭解如何在Adobe Experience Platform使用者介面中將現有結構描述匯出至其他沙箱或組織。
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 11%

---

# 在 UI 中匯出 XDM 結構描述 {#export-xdm-schemas-in-the-UI}

>[!CONTEXTUALHELP]
>id="platform_xdm_copyjsonstructure"
>title="複製 JSON 結構"
>abstract="透過將 JSON 結構複製到剪貼簿，為您所選的結構描述產生匯出承載。使用此功能可以匯出結構描述庫中任何結構描述的詳細資訊。然後，可以使用匯出的 JSON 將結構描述和任何相關資源匯入到不同的沙箱或組織。如此可在不同環境之間的模式輕鬆且有效率地共用和重複使用結構描述。"

結構描述資料庫中的所有資源都包含在組織內的特定沙箱中。 在某些情況下，您可能會想要在沙箱和組織之間共用Experience Data Model (XDM)資源。

為了滿足此需求，Adobe Experience Platform UI中的[!UICONTROL 結構描述]工作區可讓您為結構描述資料庫中的任何結構描述產生匯出裝載。 然後，此裝載可用於對結構描述登入API的呼叫中，以將結構描述（以及所有相依資源）匯入目標沙箱和組織。

>[!NOTE]
>
>您也可以使用Schema Registry API來匯出結構描述以外的其他資源，包括類別、結構描述欄位群組和資料型別。 如需詳細資訊，請參閱[匯出端點指南](../api/export.md)。

## 先決條件

雖然Platform UI可讓您匯出XDM資源，但您必須使用結構描述登入API將這些資源匯入其他沙箱或組織以完成工作流程。 在遵循本指南之前，請參閱[架構登入API快速入門](../api/getting-started.md)指南，以取得有關所需驗證標頭的重要資訊。

## 產生匯出裝載 {#generate-export-payload}

匯出裝載可在Platform UI中從[!UICONTROL 瀏覽]標籤的詳細資訊面板產生，或直接從結構描述編輯器中的結構描述畫布產生。

若要產生匯出裝載，請在左側導覽中選取&#x200B;**[!UICONTROL 結構描述]**。 在[!UICONTROL 結構描述]工作區中，選取您要匯出的結構描述列，以在右側邊欄中顯示結構描述詳細資訊。

>[!TIP]
>
>請參閱[探索XDM資源](./explore.md)的指南，以取得有關如何尋找您所尋找XDM資源的詳細資訊。

接著，從可用選項中選取&#x200B;**[!UICONTROL 複製JSON]**&#x200B;圖示（![復製圖示](/help/images/icons/copy.png)）。

![包含結構描述列和[!UICONTROL 複製到JSON]的結構描述工作區已反白顯示。](../images/ui/export/copy-json.png)

這樣會根據結構描述結構產生JSON裝載並複製到剪貼簿。 針對上述的「[!DNL Loyalty Members]」結構描述，會產生下列JSON：

+++選取以展開範例JSON裝載

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

+++

也可以透過選取結構描述編輯器右上角的[!UICONTROL 更多]來複製裝載。 下拉式功能表提供兩個選項：[!UICONTROL 複製JSON結構]和[!UICONTROL 刪除結構描述]。

>[!NOTE]
>
>為設定檔啟用結構描述或具有關聯的資料集時，無法刪除結構描述。

![包含[!UICONTROL 更多]和[!UICONTROL 複製到JSON]的結構描述編輯器已強調顯示。](../images/ui/export/schema-editor-copy-json.png)

裝載採用陣列形式，每個陣列專案都是代表要匯出的自訂XDM資源的物件。 在上述範例中，已包含&quot;[!DNL Loyalty details]&quot;自訂欄位群組和&quot;[!DNL Loyalty Members]&quot;結構描述。 結構描述採用的任何核心資源都不會包含在匯出中，因為這些資源可用於所有沙箱和組織。

請注意，您組織的租使用者ID的每個例項在承載中顯示為`<XDM_TENANTID_PLACEHOLDER>`。 這些預留位置會自動取代為適當的租使用者ID值，具體取決於您在下一個步驟匯入結構描述的位置。

## 使用API匯入資源 {#import-resource-with-api}

一旦您複製了結構描述的匯出JSON後，您就可以將它當做結構描述登入API中`/rpc/import`端點的POST要求裝載。 請參閱[匯入端點指南](../api/import.md)，以取得有關如何設定呼叫以將結構描述傳送至所需組織和沙箱的詳細資訊。

## 後續步驟

依照本指南，您已成功將XDM結構描述匯出至不同的組織或沙箱。 如需[!UICONTROL 結構描述] UI功能的詳細資訊，請參閱[[!UICONTROL 結構描述] UI概觀](./overview.md)。
