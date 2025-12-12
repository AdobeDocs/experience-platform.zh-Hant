---
title: Personalization組態設定
description: 在網頁SDK標籤擴充功能中設定個人化設定。
source-git-commit: 9a617b6e97aec22a6726266f2628bd2c2a05da19
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# Personalization組態設定

此設定區段可讓您決定在載入個人化內容時如何隱藏頁面的某些部分。 正確設定後，這些設定可確保您的訪客看到正確的個人化內容。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下捲動至&#x200B;**[!UICONTROL Personalization]**&#x200B;區段。

![此影像顯示標籤使用者介面中Web SDK標籤擴充功能的個人化設定](../assets/web-sdk-ext-personalization.png)

提供下列選項：

## [!UICONTROL Migrate Target from at.js to the Web SDK]**

使用此選項可允許Web SDK讀取和寫入`mbox` 1.x或2.x程式庫使用的舊版`mboxEdgeCluster`和`at.js` Cookie。 此設定有助於在使用Web SDK或相同網站上的`at.js`在頁面之間移動時保持訪客設定檔不變。 如果您的網站上的任何地方都未實作`at.js`，則不需要啟用此核取方塊。 此核取方塊的JavaScript資料庫等同於[`targetMigrationEnabled`](/help/collection/js/commands/configure/targetmigrationenabled.md)。

啟用此選項時，請確定您在[`overrideMboxEdgeServer`中也啟用](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver)`targetGlobalSettings()`。

## [!UICONTROL Prehiding style] {#prehiding-style}

預先隱藏樣式編輯器可讓您定義自訂CSS規則，以隱藏頁面的特定區段。 載入頁面時，網頁SDK會使用此樣式來隱藏需要個人化的區段，擷取個人化，然後取消隱藏個人化的頁面區段。 此工作流程可讓訪客檢視個人化內容，而不會看到個人化擷取程式載入或閃爍。 與此程式碼編輯器相當的JavaScript程式庫是[`prehidingStyle`](/help/collection/js/commands/configure/prehidingstyle.md)。

## [!UICONTROL Prehiding snippet] {#prehiding-snippet}

本節並非直接的組態設定，而是方便您取得實作程式碼的位置。 在您的網站上的`<head>`標籤中實作此預先隱藏程式碼片段，以便在載入Web SDK程式庫時隱藏所需的內容。

>[!IMPORTANT]
>
>使用預先隱藏程式碼片段時，Adobe建議在預先隱藏程式碼片段和預先隱藏樣式之間使用相同的CSS規則。

## [!UICONTROL Enable personalization storage]

允許網頁SDK儲存個人化事件的核取方塊。 位於瀏覽器的本機儲存空間中。 如果您想要追蹤訪客在各個頁面載入間看過的體驗，這個維度就十分實用。

## [!UICONTROL Auto click collection for Adobe Journey Optimizer]

一個下拉式功能表，可決定Web SDK何時自動收集從Adobe Journey Optimizer傳回內容的點按次數。

* **[!UICONTROL Always]**：收集與主張的所有互動。
* **[!UICONTROL Decorated elements only]**：僅收集具有`data-aep-click-label`或`data-aep-click-token`個HTML屬性之元素的互動。
* **[!UICONTROL Never]**：不要收集與主張的互動。

此下拉式功能表的JavaScript程式庫等同於[`autoCollectPropositionInteractions.AJO`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md)。 其預設值為[!UICONTROL Always]。

## [!UICONTROL Auto click collection for Adobe Target]

一個下拉式功能表，可決定Web SDK何時自動收集從Adobe Target傳回內容的點按次數。

* **[!UICONTROL Always]**：收集與主張的所有互動。
* **[!UICONTROL Decorated elements only]**：僅收集具有`data-aep-click-label`或`data-aep-click-token`個HTML屬性之元素的互動。
* **[!UICONTROL Never]**：不要收集與主張的互動。

此下拉式功能表的JavaScript程式庫等同於[`autoCollectPropositionInteractions.TGT`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md)。 其預設值為[!UICONTROL Never]。
