---
title: 資料彙集組態設定
description: 在網頁SDK標籤擴充功能中設定資料收集設定。
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# 資料彙集組態設定

此設定區段可讓您決定如何跨擴充功能收集資料。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下捲動至&#x200B;**[!UICONTROL Data collection]**&#x200B;區段。

![此影像顯示標籤UI中Web SDK標籤擴充功能的資料收集設定。](../assets/web-sdk-ext-collection.png)

提供下列選項：

## [!UICONTROL On before event send callback]

回呼函式可評估及修改傳送至Adobe的裝載。 在程式碼編輯器中，您可以存取下列變數：

* **`content.xdm`**：事件的XDM裝載。
* **`content.data`**：事件的資料物件承載。
* **`return true`**：立即結束回呼，並以`content`物件中的目前值傳送資料至Adobe。
* **`return false`**：立即結束回呼並中止傳送資料至Adobe。

任何在`content`外部定義的變數都可以使用，但不包含在傳送至Adobe的裝載中。

>[!WARNING]
>
>此回呼允許使用自訂程式碼。 如果您包含在回呼中的任何程式碼擲回未攔截到的例外狀況，處理事件時就會中止。 **資料未傳送至Adobe。**

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>避免在頁面上的第一個事件上傳回`false`。 在第一個事件中傳回`false`可能會對個人化產生負面影響。

此回呼的標籤相當於JavaScript資料庫中的[`onBeforeEventSend`](/help/collection/js/commands/configure/onbeforeeventsend.md)。

## [!UICONTROL Collect internal link clicks]

此核取方塊可讓您收集網站或屬性內部的連結追蹤資料。 此核取方塊相當於JavaScript資料庫中的[`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md)標籤。 啟用此核取方塊時，會顯示事件分組選項：

* **[!UICONTROL No event grouping]**：連結追蹤資料會以個別事件傳送至Adobe。 在個別事件中傳送的連結點選可能會增加傳送至Adobe Experience Platform的資料的合約使用量。
* **[!UICONTROL Event grouping using session storage]**：將連結追蹤資料儲存在工作階段存放區，直到下一個「頁面檢視」事件為止。 在下一個視為「頁面檢視」的事件中，儲存的連結追蹤資料會與「頁面檢視」事件裝載合併。 Adobe建議在追蹤內部連結時啟用此設定。
* **[!UICONTROL Event grouping using local object]**：將連結追蹤資料儲存在本機物件中，直到下一個「頁面檢視」事件為止。 如果訪客導覽至新的瀏覽器頁面，連結追蹤資料會遺失。 此設定在單頁應用程式環境中最為有利。

當裝載中包含下列元素時，標籤程式庫會將指定事件視為「頁面檢視」：

* `xdm.web.webPageDetails.name`包含字串值
* `xdm.web.webPageDetails.pageViews.value`大於`0`

## [!UICONTROL Collect external link clicks]

啟用收集外部連結的核取方塊。 此核取方塊相當於JavaScript資料庫中的[`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md)標籤。

## [!UICONTROL Collect download link clicks]

啟用收集下載連結的核取方塊。 此核取方塊相當於JavaScript資料庫中的[`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md)標籤。

## [!UICONTROL Download link qualifier]

限定連結URL為下載連結的規則運算式。 此字串的標籤相當於JavaScript資料庫中的[`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md)。

## [!UICONTROL Filter click properties]

回呼函式可在集合前評估及修改點按相關屬性。 此函式在[!UICONTROL On before event send callback]之前執行，且標籤等同於JavaScript資料庫中的[`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md)。 在程式碼編輯器中，您可以存取下列變數：

* **`content.clickedElement`**：被點按的DOM元素。
* **`content.pageName`**：發生點選時的頁面名稱。
* **`content.linkName`**：點選連結的名稱。
* **`content.linkRegion`**：點選連結的區域。
* **`content.linkType`**：連結型別（退出、下載或其他）。
* **`content.linkURL`**：點選連結的目的地URL。
* **`return true`**：立即以目前的變數值結束回呼。
* **`return false`**：立即結束回呼並中止資料收集。
* 任何在`content`外部定義的變數都可以使用，但不包含在傳送至Adobe的裝載中。

>[!TIP]
>
>**[!UICONTROL On before link click send]**&#x200B;欄位是已棄用的回呼，只會顯示給已設定它的屬性。 它等同於JavaScript資料庫中的[`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md)標籤。 使用&#x200B;**[!UICONTROL Filter click properties]**&#x200B;回撥來篩選或調整點選資料，或使用&#x200B;**[!UICONTROL On before event send callback]**&#x200B;來篩選或調整傳送至Adobe的整體裝載。 如果&#x200B;**[!UICONTROL Filter click properties]**&#x200B;回呼和&#x200B;**[!UICONTROL On before link click send]**&#x200B;回呼皆已設定，則只有&#x200B;**[!UICONTROL Filter click properties]**&#x200B;回呼會執行。

## 內容設定

自動收集訪客資訊，這會為您填入特定XDM欄位。 您可以選擇&#x200B;**[!UICONTROL All default context information]**&#x200B;或&#x200B;**[!UICONTROL Specific context information]**。 它等同於JavaScript資料庫中的[`context`](/help/collection/js/commands/configure/context.md)標籤。

* **[!UICONTROL Web]**：收集目前頁面的相關資訊。
* **[!UICONTROL Device]**：收集使用者裝置的相關資訊。
* **[!UICONTROL Environment]**：收集使用者瀏覽器的相關資訊。
* **[!UICONTROL Place context]**：收集有關使用者位置的資訊。
* **[!UICONTROL High entropy user-agent hints]**：收集使用者裝置的詳細資訊。
