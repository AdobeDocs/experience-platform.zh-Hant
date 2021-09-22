---
title: 使用Adobe Experience Platform Web SDK處理客戶同意資料
topic-legacy: getting started
description: 了解如何整合Adobe Experience Platform Web SDK，以在Adobe Experience Platform中處理客戶同意資料。
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 69e510c9a0f477ad7cab530128c6728f68dfdab1
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 0%

---

# 整合Platform Web SDK以處理客戶同意資料

Adobe Experience Platform Web SDK可讓您擷取同意管理平台(CMP)產生的客戶同意訊號，並在同意變更事件發生時將其傳送至Adobe Experience Platform。

**SDK不會與任何現成可用的CMP進行介面**。您可自行決定如何將SDK整合至您的網站、接聽CMP中的同意變更，並呼叫適當的命令。 本檔案提供如何將CMP與Platform Web SDK整合的一般指引。

## 先決條件 {#prerequisites}

本教學課程假設您已決定如何在CMP中產生同意資料，且已建立包含同意欄位的資料集，這些欄位符合Adobe標準或IAB透明與同意架構(TCF)2.0標準。 如果您尚未建立此資料集，請先參閱下列教學課程，再回到本指南：

* [使用Adobe標準建立資料集](./adobe/dataset.md)
* [使用TCF 2.0標準建立資料集](./iab/dataset.md)

本指南遵循使用資料收集UI中的標籤擴充功能來設定SDK的工作流程。 如果您不想使用擴充功能，而想要在網站上直接內嵌獨立版本的SDK，請參閱下列檔案，而非本指南：

* [設定資料流](../../../edge/fundamentals/datastreams.md)
* [安裝SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [為同意命令配置SDK](../../../edge/consent/supporting-consent.md)

本指南中的安裝步驟需要妥善了解標籤擴充功能，以及這些擴充功能在網頁應用程式中的安裝方式。 如需詳細資訊，請參閱下列檔案：

* [標記總覽](../../../tags/home.md)
* [快速入門手冊](../../../tags/quick-start/quick-start.md)
* [發佈概觀](../../../tags/ui/publishing/overview.md)

## 設定資料流

為了讓SDK將資料傳送至Experience Platform，您必須先設定資料流。 在資料收集UI中，在左側導覽中選取&#x200B;**[!UICONTROL 資料流]**。

建立新資料流或選取要編輯的現有資料流後，請選取&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;旁的切換按鈕。 接下來，使用下列值填寫表單。

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| 資料流欄位 | 值 |
| --- | --- |
| [!UICONTROL 沙箱] | 平台[sandbox](../../../sandboxes/home.md)的名稱，其中包含設定資料流所需的串流連線和資料集。 |
| [!UICONTROL 串流入口] | 有效的串流連線，用於Experience Platform。 如果您沒有現有的串流入口，請參閱有關[建立串流連接](../../../ingestion/tutorials/create-streaming-connection-ui.md)的教程。 |
| [!UICONTROL 事件資料集] | 您打算使用SDK將事件資料傳送至的[!DNL XDM ExperienceEvent]資料集。 雖然您必須提供事件資料集才能建立Platform資料流，請注意，下游實施工作流程不會遵循透過事件傳送的同意資料。 |
| [!UICONTROL 設定檔資料集] | 已啟用[!DNL Profile]且您建立[eler](#prerequisites)之客戶同意欄位的資料集。 |

完成後，在螢幕底部選擇&#x200B;**[!UICONTROL Save]**，然後繼續執行任何其他提示以完成配置。

## 安裝及配置Platform Web SDK

依照前一節所述建立資料流後，您必須設定最終要部署在網站上的Platform Web SDK擴充功能。 如果您的標籤屬性上未安裝SDK擴充功能，請在左側導覽中選取「**[!UICONTROL 擴充功能]**」，然後按一下「**[!UICONTROL 目錄]**」標籤。 接著，在可用擴充功能清單的Platform SDK擴充功能下方，選取&#x200B;**[!UICONTROL 安裝]**。

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

設定SDK時，在「**[!UICONTROL Edge Configurations]**」下方，選取您在上一步驟中建立的資料流。

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

選擇&#x200B;**[!UICONTROL 保存]**&#x200B;以安裝擴展。

### 建立資料元素以設定預設同意

安裝SDK擴充功能後，您便可選擇建立資料元素，以代表使用者的預設資料收集同意值(`collect.val`)。 如果您想要根據使用者而有不同的預設值，例如歐盟使用者的`pending`和北美使用者的`in`，這個功能會很實用。

在此使用案例中，您可實作下列項目，以根據使用者的地區設定預設同意：

1. 確定Web伺服器上的用戶區域。
1. 在網頁上的`script`標籤（內嵌程式碼）之前，轉譯個別的`script`標籤，該標籤會根據使用者的地區設定`adobeDefaultConsent`變數。
1. 設定使用`adobeDefaultConsent` JavaScript變數的資料元素，並將此資料元素設為使用者的預設同意值。

如果使用者的地區由CMP決定，您可以改用下列步驟：

1. 處理頁面上的「CMP已載入」事件。
1. 在事件處理常式中，根據使用者的地區設定`adobeDefaultConsent`變數，然後使用JavaScript載入標籤程式庫指令碼。
1. 設定使用`adobeDefaultConsent` JavaScript變數的資料元素，並將此資料元素設為使用者的預設同意值。

若要在資料收集UI中建立資料元素，請在左側導覽中選取&#x200B;**[!UICONTROL 資料元素]**，然後選取&#x200B;**[!UICONTROL 新增資料元素]**&#x200B;以導覽至資料元素建立對話方塊。

您必須在此建立以`adobeDefaultConsent`為基礎的[!UICONTROL  JavaScript變數]資料元素。 完成後，選擇&#x200B;**[!UICONTROL Save]**。

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

建立資料元素後，請導覽回Web SDK擴充功能設定頁面。 在[!UICONTROL Privacy]區段下，選取&#x200B;**[!UICONTROL 由資料元素提供]**，然後使用提供的對話方塊選取您先前建立的預設同意資料元素。

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### 在您的網站上部署擴充功能

完成擴充功能的設定後，即可將其整合至您的網站。 如需如何部署更新的程式庫組建的詳細資訊，請參閱標籤檔案中的[發佈指南](../../../tags/ui/publishing/overview.md) 。

## 執行同意更改命令 {#commands}

將SDK擴充功能整合至網站後，您就可以開始使用Platform Web SDK `setConsent`命令，將同意資料傳送至Platform。

>[!IMPORTANT]
>
>`setConsent`命令只會直接更新設定檔存放區中的資料，不會將任何資料傳送至資料湖。

在以下兩種情況中，應在您的網站上呼叫`setConsent`:

1. 同意在頁面上載入時（亦即，在每次頁面載入時）
1. 做為CMP連結或事件接聽程式的一部分，可偵測同意設定中的變更

>[!NOTE]
>
>如需Platform SDK命令的常見語法簡介，請參閱[執行命令](../../../edge/fundamentals/executing-commands.md)的相關檔案。

`setConsent`命令需要兩個參數：

1. 指示命令類型的字串（在此例中為`"setConsent"`）
1. 包含單一陣列類型屬性的裝載物件：`consent`。 `consent`陣列必須至少包含一個物件，提供Adobe標準的必要同意欄位。

Adobe標準的必要同意欄位顯示在以下範例`setConsent`呼叫中：

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
| `standard` | 使用的同意標準。 對於Adobe標準，此值必須設定為`Adobe`。 |
| `version` | `standard`下所示的同意標準版本號。 此值必須設為`2.0`才能進行Adobe標準同意處理。 |
| `value` | 客戶更新的同意資訊，以XDM物件提供，且符合已啟用設定檔之資料集的同意欄位結構。 |

>[!NOTE]
>
>如果您搭配使用其他同意標準和`Adobe`（例如`IAB TCF`），則可為每個標準將其他物件新增至`consent`陣列。 每個物件必須包含`standard`、`version`和`value`的適當值，才能代表同意標準。

以下JavaScript提供函式的範例，該函式可處理網站上的同意偏好設定變更，以作為事件接聽程式或CMP連結中的回呼：

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

所有[!DNL Platform SDK]命令都返回指示調用是成功還是失敗的承諾。 然後，您可以將這些回應用於其他邏輯，例如向客戶顯示確認訊息。 如需特定範例，請參閱執行SDK命令指南中關於[處理成功或失敗](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure)的一節。

使用SDK成功進行`setConsent`呼叫後，您就可以使用平台UI中的設定檔檢視器，驗證資料是否正在設定檔存放區中著陸。 如需詳細資訊，請參閱[依身分瀏覽設定檔的區段](../../../profile/ui/user-guide.md#browse-identity)。

## 後續步驟

依照本指南，您已設定Platform Web SDK擴充功能，將同意資料傳送至Experience Platform。 如需測試實作的指引，請參閱要實作之同意標準的檔案：

* [Adobe標準](./adobe/overview.md#test)
* [TCF 2.0標準](./iab/overview.md#test)
