---
title: 使用Adobe Experience PlatformWeb SDK處理客戶同意資料
topic-legacy: getting started
description: 瞭解如何整合Adobe Experience PlatformWeb SDK以處理Adobe Experience Platform的客戶同意資料。
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 79bc41c713425e14bb3c12646b9b71b2c630618b
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# 整合平台Web SDK以處理客戶同意資料

Adobe Experience PlatformWeb SDK允許您檢索由同意管理平台(CMP)生成的客戶同意信號，並在出現同意更改事件時將其發送到Adobe Experience Platform。

**SDK不與任何出廠設定的CMP進行介面**。 如何將SDK整合到您的網站、傾聽CMP中的同意更改並調用相應的命令，由您決定。 本文檔提供有關如何將CMP與平台Web SDK整合的一般指導。

## 先決條件 {#prerequisites}

本教程假定您已確定如何在CMP中生成同意資料，並已建立了包含符合Adobe標準或IAB透明度和同意框架(TCF)2.0標準的同意欄位的資料集。 如果尚未建立此資料集，請在返回本指南之前參閱以下教程：

* [使用Adobe標準建立資料集](./adobe/dataset.md)
* [使用TCF 2.0標準建立資料集](./iab/dataset.md)

本指南遵循使用資料收集UI中的標籤擴展設定SDK的工作流。 如果您不想使用副檔名，並且希望直接在您的站點上嵌入SDK的獨立版本，請參閱以下文檔，而不是本指南：

* [配置資料流](../../../edge/datastreams/overview.md)
* [安裝SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [配置SDK以執行同意命令](../../../edge/consent/supporting-consent.md)

本指南中的安裝步驟要求您瞭解標籤擴展以及它們在Web應用程式中的安裝方式。 有關詳細資訊，請參閱以下文檔：

* [標記總覽](../../../tags/home.md)
* [快速入門手冊](../../../tags/quick-start/quick-start.md)
* [發佈概觀](../../../tags/ui/publishing/overview.md)

## 設定資料流

為了使SDK將資料發送到Experience Platform，必須首先配置資料流。 在資料收集UI中，選擇 **[!UICONTROL 資料流]** 的子菜單。

建立新資料流或選擇要編輯的現有資料流後，選擇旁邊的切換按鈕 **[!UICONTROL Adobe Experience Platform]**。 接下來，使用下面列出的值完成表單。

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| 資料流欄位 | 值 |
| --- | --- |
| [!UICONTROL 沙箱] | 平台的名稱 [沙坑](../../../sandboxes/home.md) 包含設定資料流所需的流連接和資料集。 |
| [!UICONTROL 流式入口] | 用於Experience Platform的有效流連接。 請參閱上的教程 [建立流連接](../../../ingestion/tutorials/create-streaming-connection-ui.md) 如果沒有現有的流入口。 |
| [!UICONTROL 事件資料集] | 安 [!DNL XDM ExperienceEvent] 您計畫使用SDK將事件資料發送到的資料集。 雖然需要您提供事件資料集以建立平台資料流，但請注意，下游實施工作流中不遵守通過事件發送的同意資料。 |
| [!UICONTROL 配置檔案資料集] | 的 [!DNL Profile] — 啟用的資料集，包含您建立的客戶同意欄位 [早](#prerequisites)。 |

完成後，選擇 **[!UICONTROL 保存]** 在螢幕底部，繼續執行任何附加提示以完成配置。

## 安裝和配置平台Web SDK

建立上一節所述的資料流後，必須配置最終將在站點上部署的平台Web SDK擴展。 如果您的tag屬性上未安裝SDK擴展，請選擇 **[!UICONTROL 擴展]** 在左側的導航欄中，然後是 **[!UICONTROL 目錄]** 頁籤。 然後，選擇 **[!UICONTROL 安裝]** 在「平台SDK擴展」下。

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

配置SDK時，在 **[!UICONTROL 邊緣配置]**，選擇在上一步中建立的資料流。

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

選擇 **[!UICONTROL 保存]** 安裝擴展。

### 建立資料元素以設定預設同意

安裝SDK擴展後，您可以選擇建立資料元素來表示預設資料收集同意值(`collect.val`)。 如果您希望根據用戶具有不同的預設值，如 `pending` 為歐盟用戶和 `in` 北美用戶。

在此使用情形中，您可以實施以下操作來根據用戶區域設定預設同意：

1. 確定Web伺服器上的用戶區域。
1. 在 `script` 標籤（嵌入代碼），呈現單獨的 `script` 設定 `adobeDefaultConsent` 變數基於用戶區域。
1. 設定使用 `adobeDefaultConsent` JavaScript變數，並將此資料元素用作用戶的預設同意值。

如果用戶的區域由CMP確定，則可以改用以下步驟：

1. 處理頁面上的「CMP載入」事件。
1. 在事件處理程式中，設定 `adobeDefaultConsent` 變數，然後使用JavaScript載入標籤庫指令碼。
1. 設定使用 `adobeDefaultConsent` JavaScript變數，並將此資料元素用作用戶的預設同意值。

要在資料收集UI中建立資料元素，請選擇 **[!UICONTROL 資料元素]** 在左側導航中，然後選擇 **[!UICONTROL 添加資料元素]** 導航至資料元素建立對話框。

在此，必須建立 [!UICONTROL JavaScript變數] 資料元 `adobeDefaultConsent`。 選擇 **[!UICONTROL 保存]** 的子菜單。

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

建立資料元素後，導航回Web SDK擴展配置頁。 在 [!UICONTROL 隱私] 選擇 **[!UICONTROL 由資料元素提供]**，並使用提供的對話框選擇先前建立的預設同意資料元素。

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### 在您的網站上部署擴展

配置完擴展後，可將其整合到您的網站中。 請參閱 [發佈指南](../../../tags/ui/publishing/overview.md) 的子常式。

## 生成同意更改命令 {#commands}

將SDK擴展整合到網站後，可以開始使用平台Web SDK `setConsent` 命令向平台發送同意資料。

的 `setConsent` 命令執行兩個操作：

1. 直接在配置檔案儲存中更新用戶的配置檔案屬性。 這不會向資料湖發送任何資料。
1. 建立 [體驗事件](../../../xdm/classes/experienceevent.md) 記錄了同意更改事件的時間戳記。 此資料直接發送到資料湖，並可用於跟蹤隨時間變化的同意偏好變化。

### 何時打電話 `setConsent`

有兩種情況 `setConsent` 應在您的站點上調用：

1. 當同意載入到頁面（換句話說，在每個頁面載入上）
1. 作為檢測同意設定更改的CMP掛接或事件偵聽器的一部分

### `setConsent` 語法

>[!NOTE]
>
>有關Platform SDK命令的常用語法的介紹，請參見上的文檔 [執行命令](../../../edge/fundamentals/executing-commands.md)。

的 `setConsent` 命令需要兩個參數：

1. 指示命令類型的字串(在本例中， `"setConsent"`)
1. 包含單個陣列類型屬性的負載對象： `consent`。 的 `consent` 陣列必須至少包含一個為Adobe標準提供必需的同意欄位的對象。

Adobe標準的必需同意欄位如下例所示 `setConsent` 呼叫：

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

| 負載屬性 | 說明 |
| --- | --- |
| `standard` | 正在使用的同意標準。 對於Adobe標準，此值必須設定為 `Adobe`。 |
| `version` | 下面所示的同意標準的版本號 `standard`。 此值必須設定為 `2.0` Adobe標準同意處理。 |
| `value` | 客戶的更新的同意資訊，作為符合啟用Profile的資料集的同意欄位結構的XDM對象提供。 |

>[!NOTE]
>
>如果您使用其他同意標準 `Adobe` (例如 `IAB TCF`)，您可以向 `consent` 陣列。 每個對象必須包含適當的值 `standard`。 `version`, `value` 他們代表的同意標準。

以下JavaScript提供了一個函式示例，該函式處理網站上的同意首選項更改，該函式可用作事件偵聽器或CMP掛接中的回調：

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

## 處理SDK響應

全部 [!DNL Platform SDK] 命令返回指示調用是成功還是失敗的承諾。 然後，您可以將這些響應用於其它邏輯，如向客戶顯示確認消息。 請參閱 [處理成功或失敗](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 的子例。

成功完成後 `setConsent` 調用SDK時，您可以使用平台UI中的配置檔案查看器來驗證資料是否正登錄到配置檔案儲存中。 請參閱 [按身份瀏覽配置檔案](../../../profile/ui/user-guide.md#browse-identity) 的子菜單。

## 後續步驟

按照本指南，您已配置了平台Web SDK擴展，以將同意資料發送到Experience Platform。 有關測試實施的指導，請參閱要實施的同意標準的文檔：

* [Adobe標準](./adobe/overview.md#test)
* [TCF 2.0標準](./iab/overview.md#test)
