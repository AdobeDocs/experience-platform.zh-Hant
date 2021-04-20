---
title: 使用Adobe Experience Platform網頁SDK處理客戶同意資料
topic: getting started
description: 瞭解如何整合Adobe Experience Platform網頁SDK，以使用Adobe2.0標準處理Adobe Experience Platform的客戶同意資料。
translation-type: tm+mt
source-git-commit: fee3f005ca3679f8639cea45c16150090b2a1e0f
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 0%

---


# 整合Platform Web SDK，使用Adobe2.0標準處理客戶同意資料

Adobe Experience Platform網頁SDK可讓您擷取「同意管理平台」(CMPs)產生的客戶同意信號，並在許可變更事件發生時將其傳送至Adobe Experience Platform。

**SDK不會與任何出廠時的CMP介接**。您需自行決定如何將SDK整合至您的網站、聽取CMP中的同意變更，並呼叫適當的命令。 本檔案提供如何將CMP與Platform Web SDK整合的一般指南。

## 先決條件

本教程假定您已確定如何在CMP中生成許可資料，並建立了包含已為「即時客戶概要檔案」啟用的許可欄位的資料集。 若要進一步瞭解這些步驟，請先參閱Experience Platform](./overview.md)中的[同意處理概述，然後再返回本指南。

此外，本指南還要求您瞭解Adobe Experience Platform Launch擴充功能，以及它們在Web應用程式中的安裝方式。 如需詳細資訊，請參閱下列檔案：

* [platform launch概觀](https://experienceleague.adobe.com/docs/launch/using/home.html)
* [快速入門手冊](https://experienceleague.adobe.com/docs/launch/using/get-started/quick-start.html)
* [發佈概觀](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html)

## 設定邊緣設定

若要讓SDK傳送資料至Experience Platform，您必須有在Adobe Experience Platform Launch設定之平台的現有邊緣組態。 此外，您為配置選擇的[!UICONTROL Profile Dataset]必須包含標準化的許可欄位。

建立新配置或選取現有配置進行編輯後，請選取&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;旁的切換按鈕。 接著，使用下列值來完成表單。

![](../../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Edge configuration欄位 | 值 |
| --- | --- |
| [!UICONTROL Sandbox] | 平台[沙盒](../../../../sandboxes/home.md)的名稱，其中包含設定邊緣配置所需的串流連接和資料集。 |
| [!UICONTROL Streaming Inlet] | 有效的串流連線，以供Experience Platform。 如果您沒有現有的串流入口，請參閱有關建立串流連線的[教學課程。](../../../../ingestion/tutorials/create-streaming-connection-ui.md) |
| [!UICONTROL Event Dataset] | 您打算使用SDK傳送事件資料至的[!DNL XDM ExperienceEvent]資料集。 雖然您必須提供事件資料集才能建立平台邊緣組態，但請注意，目前不支援透過事件直接傳送同意資料。 |
| [!UICONTROL Profile Dataset] | 啟用[!DNL Profile]的資料集，包含您先前建立的客戶同意欄位。 |

完成後，選擇螢幕底部的&#x200B;**[!UICONTROL Save]** ，然後繼續執行任何其他提示以完成配置。


## 安裝及設定平台網頁SDK擴充功能

在您建立如上節所述的邊緣設定後，您必須先設定最終將部署在網站上的平台網頁SDK擴充功能。 如果您的Platform launch屬性上未安裝SDK擴充功能，請在左側導覽中選取&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Catalog]**&#x200B;標籤。 然後，在可用擴充功能清單中，選取「平台SDK擴充功能」下方的&#x200B;**[!UICONTROL Install]**。

![](../../../images/governance-privacy-security/consent/adobe/sdk/install.png)

設定SDK時，在&#x200B;**[!UICONTROL Edge Configurations]**&#x200B;下方，選取您在上一步驟中建立的設定。

![](../../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

選擇&#x200B;**[!UICONTROL Save]**&#x200B;以安裝擴展。

### 建立資料元素以設定預設同意

在安裝SDK擴充功能後，您可以選擇建立資料元素，以代表使用者的預設資料收集同意值(`collect.val`)。 如果您想要根據使用者擁有不同的預設值，例如歐盟使用者的`pending`和北美使用者的`in`，這個功能就很有用。

在此使用案例中，您可以實作下列項目，根據使用者的地區設定預設同意：

1. 確定Web伺服器上的用戶區域。
1. 在網頁上的Platform launch指令碼標籤（內嵌代碼）之前，請演算個別的指令碼標籤，以根據使用者的地區設定`adobeDefaultConsent`變數。
1. 設定使用`adobeDefaultConsent` JavaScript變數的資料元素，並將此資料元素用作使用者的預設同意值。

如果用戶的區域由CMP確定，則可以改用以下步驟：

1. 處理頁面上的「CMP已載入」事件。
1. 在事件處理常式中，根據使用者的地區設定`adobeDefaultConsent`變數，然後使用JavaScript載入Platform launch程式庫指令碼。
1. 設定使用`adobeDefaultConsent` JavaScript變數的資料元素，並將此資料元素用作使用者的預設同意值。

若要在Platform launchUI中建立資料元素，請在左側導覽中選取&#x200B;**[!UICONTROL Data Elements]**，然後選取&#x200B;**[!UICONTROL Add Data Element]**&#x200B;以導覽至資料元素建立對話方塊。

從這裡，您必鬚根據`adobeDefaultConsent`建立[!UICONTROL JavaScript Variable]資料元素。 完成後選取「**[!UICONTROL Save]**」。

![](../../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

建立資料元素後，請導覽回網頁SDK擴充功能設定頁面。 在[!UICONTROL Privacy]節下，選擇&#x200B;**[!UICONTROL Provided by data element]** ，然後使用提供的對話框選擇您先前建立的預設許可資料元素。

![](../../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### 在您的網站上部署擴充功能

在您完成擴充功能的設定後，就可將它整合在您的網站中。 請參閱Platform launch檔案中的[發佈指南](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html)，以取得有關如何部署更新程式庫組建版本的詳細資訊。

## 進行許可更改命令

將SDK擴充功能整合至網站後，您就可開始使用「平台網頁SDK `setConsent`」命令，將同意資料傳送至「平台」。

在您的網站上應呼叫`setConsent`的兩種情況：

1. 當同意書載入頁面時（換言之，每次載入頁面時）
1. 作為CMP掛接或事件偵聽器的一部分，該偵聽器檢測許可設定中的更改

>[!NOTE]
>
>有關Platform SDK命令的常見語法的簡介，請參閱[執行命令](../../../../edge/fundamentals/executing-commands.md)上的檔案。

`setConsent`命令需要兩個參數：

1. 指示命令類型的字串（在本例中為`"setConsent"`）
1. 包含單一陣列類型屬性的裝載對象：`consent`。 `consent`陣列必須至少包含一個對象，該對象為Adobe標準提供必要的許可欄位。

Adobe標準的必要許可欄位如以下示例`setConsent`調用中所示：

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| 裝載屬性 | 說明 |
| --- | --- |
| `standard` | 使用許可標準。 對於Adobe標準，此值必須設定為`Adobe`。 |
| `version` | `standard`下所示同意標準的版本號。 此值必須設為`2.0`才能進行Adobe標准許可處理。 |
| `value` | 客戶的更新許可資訊，作為XDM對象提供，該XDM對象符合啟用配置檔案的資料集的許可欄位的結構。 |

>[!NOTE]
>
>如果您正在與`Adobe`（例如`IAB TCF`）一起使用其他許可標準，則可以為每個標準向`consent`陣列添加其他對象。 每個對象必須包含`standard`、`version`和`value`的適當值，以表示其表示的許可標準。

以下JavaScript提供一個函式範例，該函式可處理網站上的同意偏好變更，可用作事件接聽程式或CMP掛接中的回呼：

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## 處理SDK回應

所有[!DNL Platform SDK]命令都返回表示呼叫是成功還是失敗的承諾。 然後，您可以將這些回應用於其他邏輯，例如向客戶顯示確認訊息。 如需特定範例，請參閱執行SDK命令指南中有關[處理成功或失敗的章節。](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure)

## 後續步驟

依照本指南，您已設定平台網頁SDK擴充功能，以傳送同意資料給Experience Platform。 您現在可以返回同意處理概述，以取得如何[測試實作的步驟](./overview.md#test-implementation)。