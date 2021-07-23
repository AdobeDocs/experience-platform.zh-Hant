---
title: Adobe MediumAnalytics(3.x SDK)for Audio and Video擴充功能概述
description: 了解Adobe Experience Platform中的Adobe MediumAnalytics(3.x SDK)for Audio and Video標籤擴充功能。
source-git-commit: 7f694310b17ab257eae459003bb820f7221bb55e
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 73%

---

# Adobe MediumAnalytics(3.x SDK)for Audio and Video擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../../term-updates.md)。

本文件主要說明安裝、設定和實作 Adobe Media Analytics (3.x SDK) for Audio and Video 擴充功能 (Media Analytics 擴充功能) 的相關資訊，其中包含使用此擴充功能來建立規則時可用的選項，以及範例和範例連結。

Media Analytics (MA) 擴充功能新增核心 JavaScript Media SDK (Media 3.x SDK)。此擴充功能提供將`Media`追蹤器例項新增至已啟用標籤之網站或專案的功能。 MA 擴充功能需要額外的擴充功能：

* [Analytics 擴充功能](../analytics/overview.md)
* [Experience Cloud ID 擴充功能](../id-service/overview.md)

>[!IMPORTANT]
>
>此擴充功能會與 Media 3.x SDK 一併部署，且無法向下相容於 Media 2.x SDK。如果您的頁面已使用 Media 2.x SDK，請改用 [Adobe Media Analytics for Audio and Video Extension](../media-analytics/overview.md)，而非此擴充功能。

在您的標籤啟用專案中納入上述的三個擴充功能後，您可以透過下列兩種方式之一繼續操作：

* 從您的網頁應用程式使用 `Media` API
* 納入或建立播放器特定的擴充功能，此模組會將特定的媒體播放器事件對應到 `Media` 追蹤器例項上的 API。此例項會透過 MA 擴充功能公開。

## 安裝並設定 MA 擴充功能

* **安裝：** 若要安裝MA擴充功能，請開啟您的擴充功能屬性，選取「擴充 **[!UICONTROL 功能>目錄]**」，將游標暫留在 **[!UICONTROL 「Adobe Medium分析(3.x SDK)for Audio and Videoextension」上，然]** 後選取「 **[!UICONTROL 安裝]**」。

* **設定：** 若要設定MA擴充功能，請開啟「擴充  功能」標籤、將游標暫留在擴充功能上，然後選 **[!UICONTROL 取「設定」]**:

![MA 擴充功能設定](../../../images/ext-ma-config.png)

### 設定選項：

| 選項 | 說明 |
| :--- | :--- |
| Collection API Server | 定義 Media Collection API 伺服器 (請連絡您的 Adobe 代表以取得此伺服器) |
| Application Version | 媒體播放器應用程式/SDK 的版本 |
| Player Name | 使用的媒體播放器名稱 (例如：「AVPlayer」、「HTML5 播放器」、「我的自訂視訊播放器」) |
| Channel | 管道名稱屬性 |
| Debug Logging | 啟用或停用記錄 |
| Enable SSL | 啟用或停用透過 HTTPS 傳送 Ping |
| Export APIs to Window Object | 啟用或停用將 Media Analytics API 匯出至全域範圍 |
| Variable Name | 用來匯出 `window` 物件下 Media Analytics API 的變數 |

**提醒：** MA 擴充功能需有 [ Analytics](../analytics/overview.md) 和 [Experience Cloud ID](../id-service/overview.md) 擴充功能，才能正常運作。您也必須將這些擴充功能新增至擴充功能屬性並加以設定。

## 使用 MA 擴充功能

### 從網頁/JS 應用程式使用

MA擴充功能會啟用[!UICONTROL Configuration]頁面中的「將API匯出至視窗物件」設定，以匯出全域視窗物件中的媒體API。 這會以設定的變數名稱匯出 API。例如，如果變數名稱設為 `ADB`，則可使用 `window.ADB.Media` 來存取 Media API。

>[!IMPORTANT]
>
> MA 擴充功能僅會在 `window["CONFIGURED_VARIABLE_NAME"]` 未定義時匯出 API，不會覆寫現有變數。

1. **Media API：** `window["CONFIGURED_VARIABLE_NAME"].Media`

   Media SDK 的所有 API 和常數都會公開：[https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **建立 Media 追蹤器例項：** `window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **傳回值：追蹤媒體工作階段的**&#x200B;一種`Media`追蹤器例項。

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. 使用媒體追蹤器例項，並按照 [JS API 文件](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html)所述來實作媒體追蹤功能。

範例播放器可從這裡取得：[MA 範例播放器](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x)。範例播放器可作為參考，以示範如何使用 MA 擴充功能直接從網路應用程式支援 Media Analytics。


### 從其他擴充功能使用

MA擴充功能會公開`media`，作為其他擴充功能的共用模組。 (如需共用模組的其他資訊，請參閱[共用模組文件](../../../extension-dev/web/shared.md))。

>[!IMPORTANT]
>
> 共用模組只能從其他擴充功能存取。也就是說，網頁/JavaScript 應用程式無法存取共用模組，或在擴充功能之外使用 `turbine` (請參閱以下程式碼範例)。

1. **Media API：**`media`共用模組

   Media SDK 的所有 API 和常數都會公開：[https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. 建立 Media 追蹤器例項，如下所示：

   **傳回值：追蹤媒體工作階段的**&#x200B;一種`Media`追蹤器例項。

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. 使用媒體追蹤器例項，並按照 [JS API 文件](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html)所述來實作媒體追蹤功能。

>[!NOTE]
>
>**測試：**&#x200B;若要在這個版本中測試擴充功能，您必須將其上傳至 [ Platform ](../../../extension-dev/submit/upload-and-test.md)以便在其中存取所有相依的擴充功能。
