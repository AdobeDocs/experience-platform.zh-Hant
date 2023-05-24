---
title: Adobe Medium音頻和視頻擴展分析概述
description: 瞭解Adobe Experience Platform的Adobe Medium分析音頻和視頻標籤擴展。
exl-id: 426cfd08-aead-4b35-824c-45494bca2fc8
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 82%

---

# Adobe Medium音頻和視頻擴展分析概述

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

使用本文件來了解安裝、設定和實作 Adobe Media Analytics for Audio and Video 擴充功能 (Media Analytics 擴充功能) 的相關資訊其中包含使用此擴充功能來建立規則時可用的選項，以及範例和範例連結。

Media Analytics (MA) 擴充功能新增核心的 JavaScript Media SDK (Media 2.x SDK)。此擴展提供了添加 `MediaHeartbeat` 跟蹤器實例到標籤站點或項目。 MA 擴充功能需要額外的擴充功能：

* [Analytics 擴充功能](../analytics/overview.md)
* [Experience Cloud ID 擴充功能](../id-service/overview.md)

>[!IMPORTANT]
>
> 音訊追蹤功能需有 Analytics 擴充功能 v1.6 或更高版本，才能正常運作。

在標籤項目中包含了上述所有三個擴展後，可以通過以下兩種方式之一繼續：

* 從您的網頁應用程式使用 `MediaHeartbeat` API
* 納入或建立播放器特定的擴充功能，此模組會將特定的媒體播放器事件對應到 `MediaHeartbeat` 追蹤器例項上的 API。此例項會透過 MA 擴充功能公開。

## 安裝並設定 MA 擴充功能

* **安裝 —** 要安裝MA擴展，請開啟擴展屬性，選擇 **[!UICONTROL 擴展>目錄]**，懸停在 **[!UICONTROL Adobe Medium音頻和視頻分析]** 擴展，然後選擇 **[!UICONTROL 安裝]**。

* **配置 —** 要配置MA擴展，請開啟 [!UICONTROL 擴展] 頁籤，懸停在擴展上，然後選擇 **[!UICONTROL 配置]**:

![MA 擴充功能設定](../../../images/ext-va-config.jpg)

### 設定選項：

| 選項 | 說明 |
| :--- | :--- |
| Tracking Server | 定義用於追蹤媒體心率的伺服器 (此伺服器與您的 Analytics 追蹤伺服器不同) |
| Application Version | 媒體播放器應用程式/SDK 的版本 |
| Player Name | 使用的媒體播放器名稱 (例如：「AVPlayer」、「HTML5 播放器」、「我的自訂視訊播放器」) |
| Channel | 管道名稱屬性 |
| Online Video Provider | 線上視訊平台的名稱，透過該平台來分送內容 |
| Debug Logging | 啟用或停用記錄 |
| Enable SSL | 啟用或停用透過 HTTPS 傳送 Ping |
| Export APIs to Window Object | 啟用或停用將 Media Analytics API 匯出至全域範圍 |
| Variable Name | 用來匯出 `window` 物件下 Media Analytics API 的變數 |

**提醒：** MA 擴充功能需有 [ Analytics](../analytics/overview.md) 和 [Experience Cloud ID](../id-service/overview.md) 擴充功能，才能正常運作。您也必須將這些擴充功能新增至擴充功能屬性並加以設定。

## 使用 MA 擴充功能

### 從網頁/JS 應用程式使用

MA擴展通過啟用「將API導出到窗口對象」中的「將API導出到窗口對象」設定來導出全局窗口對象中的MediaHeartapt API [!UICONTROL 配置] 的子菜單。 這會以設定的變數名稱匯出 API。例如，如果變數名稱設定為 `ADB`，則可使用 `window.ADB.MediaHeartbeat` 來存取 MediaHeartbeat。

>[!IMPORTANT]
>
> MA 擴充功能僅會在 `window["CONFIGURED_VARIABLE_NAME"]` 未定義時匯出 API，不會覆寫現有變數。

1. **建立 MediaHeartbeat 例項：** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance`

   **參數：**&#x200B;有效的委派物件會顯示以下函數。

   | 方法 |  說明 |
   | :--- | :--- |
   | `getQoSObject()` | 傳回包含目前 QoS 資訊的 `theMediaObject` 例項。將在播放工作階段期間呼叫此方法多次。播放器實作必須一律傳回最新可用的 QoS 資料。 |
   | `getCurrentPlaybackTime()` | 傳回播放點的目前位置。對於 VOD 追蹤，該值是從媒體項目的開頭開始以秒為單位指定的。對於 LIVE/LIVE 追蹤，該值是從節目的開頭開始以秒為單位指定的。 |

   **傳回值：**&#x200B;一種 Promise，使用 `MediaHeartbeat` 例項解析，或拒絕並提供錯誤訊息。

1. **存取 MediaHeartbeat 常數：** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat`

   這會公開 [`MediaHeartbeat`](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) 類別中的所有常數和靜態方法。

   範例播放器可從這裡取得：[MA 範例播放器](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/2.x)。範例播放器可作為參考，以示範如何使用 MA 擴充功能直接從網路應用程式支援 Media Analytics。

1. 建立 MediaHeartbeat 追蹤器例項，如下所示：

   ```javascript
   var MediaHeartbeat = window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat;
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   };
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   };
   
   var self = this;
   MediaHeartbeat.getInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   ```

### 從其他擴充功能使用

MA 擴充功能會將 `get-instance` 模組和 `media-heartbeat` 共用模組公開至其他擴充功能(如需共用模組的其他資訊，請參閱[共用模組文件](../../../extension-dev/web/shared.md))。

>[!IMPORTANT]
>
>共用模組只能從其他擴充功能存取。也就是說，網頁/JS 應用程式無法存取共用模組，或在擴充功能之外使用 `turbine` (請參閱下面的程式碼範例)。

1. **建立 MediaHeartbeat 例項：**`get-instance`共用模組

   **參數：**

   * 有效的委派物件會顯示以下函數：

      | 方法 |  說明 |
      | :--- | :--- |
      | `getQoSObject()` | 傳回包含目前 QoS 資訊的 `MediaObject` 例項。將在播放工作階段期間呼叫此方法多次。播放器實作必須一律傳回最新的可用 QoS 資料。 |
      | `getCurrentPlaybackTime()` | 傳回播放點的目前位置。對於 VOD 追蹤，該值是從媒體項目的開頭開始以秒為單位指定的。對於 LIVE/LIVE 追蹤，該值是從節目的開頭開始以秒為單位指定的。 |

   * 選用的設定物件會顯示這些屬性：

      | 屬性 | 說明 | 必填 |
      | :--- | :--- | :--- |
      | Online Video Provider | 線上視訊平台的名稱，透過該平台來分送內容。 | 否。如果存在，則會在擴充功能設定期間覆寫定義的值。 |
      | Player Name | 使用的媒體播放器名稱 (例如：「AVPlayer」、「HTML5 播放器」、「我的自訂視訊播放器」) | 否。如果存在，則會在擴充功能設定期間覆寫定義的值。 |
      | Channel | 管道名稱屬性 | 否。如果存在，則會在擴充功能設定期間覆寫定義的值。 |
   **傳回值：**&#x200B;一種 Promise，使用 `MediaHeartbeat` 例項解析，或拒絕並提供錯誤訊息。

1. **存取 MediaHeartbeat 常數：**`media-heartbeat`共用模組

   此模組會公開此類別中所有的常數和靜態方法：[https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)。

1. 建立 MediaHeartbeat 追蹤器例項，如下所示：

   ```javascript
   var getMediaHeartbeatInstance =
     turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   
   var MediaHeartbeat =
     turbine.getSharedModule('adobe-video-analytics', 'media-heartbeat');
     ...
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   }
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   }
   ...
   
   var self = this;
   getMediaHeartbeatInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       ...
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   
   ...
   ```

1. 使用 Media Heartbeat 例項，並按照 [Media SDK JS 文件](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-javascript/set-up-js-2.html)和 [JS API 文件](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html) 中的說明來實作媒體追蹤功能。

>[!NOTE]
>
>**測試：**&#x200B;若要在這個版本中測試擴充功能，您必須將其上傳至 [ Platform ](../../../extension-dev/submit/upload-and-test.md)以便在其中存取所有相依的擴充功能。


<!--
## Leveraging the sample HTML5 player

You can obtain the MA extension sample HTML5 player here: [HTML5 Sample Player](https://github.com/adobe/reactor-adobe-va-sample-player). The sample player acts as a reference to create video player extensions and to showcase using the MA extension to support media tracking.

### Sample player extension action types

This section describes the action types available in the Sample Player extension.

#### Open Video

The _Open Video_ action provides various configurations for creating and customizing an HTML5 player, providing a video to play and enabling/disabling Adobe Video Analytics tracking.

**Action Configuration / Player Settings:** Note the CSS Selector setting which specifics the `<div>` in the web page where the player is added. Note also that the _Enable Adobe Analytics_ checkbox is checked in the Analytics Settings pane.

![Player Extension Action Configuration](../../../images/ext-va-sp-action.png)

![Player Extension Action Configuration](../../../images/ext-va-sp-action1.png)

* [\[...\]/openVideo/openVideo.jsx](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/view/actions/openVideo/openVideo.jsx) -

  UI Code to configure the Action is defined here.

* [\[...\]/actions/openVideo.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/actions/openVideo.js) - This file exports a function that gets executed when the Action is triggered as part of the tag rule.

  This is a code snippet from `openVideo.js` where the `openVideo` Action is executed:

  ```javascript
    function openVideo(settings) {
        let player;
        try {
            Logger.info(LOG_TAG, `Executing action with ${JSON.stringify(settings)}`);

            player = new PlayerFacade(settings);
            PlayerStore.registerPlayer(player);
            player.load(settings.media);
        } catch (ex) {
            Logger.error(LOG_TAG, `Creating player for action openVideo failed with error ${ex.message}`);

            // Cleanup from DOM.
            if (player) {
                player.destroy();
            }
        }
    }
    ...
  ```

* [\[...\]/analytics/adobeAnalyticsProvider.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/helpers/analytics/adobeAnalyticsProvider.js) - This file implements Video Analytics tracking by using Shared Modules exposed by the VA extension.

### Sample player extension basic deployment

Once the Sample Player extension is installed, you'll need to create at least one rule to properly deploy it. The Image below shows a sample rule that opens the specified video when the core extension fires the `DOMLoaded` event.

![Player Extension Sample Rule](../../../images/ext-va-sp-rule.png)

After you have saved this rule, you will need to add it to a Library, and then build and deploy so that you can test the behavior.

-->
