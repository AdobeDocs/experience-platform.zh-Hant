---
title: 傳送事件
description: 將資料傳送至Adobe Experience Platform Edge Network。
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# 傳送事件

**[!UICONTROL Send event]**&#x200B;動作會將裝載傳送至Adobe Experience Platform Edge Network上的資料流。 這是資料收集與個人化的核心功能；幾乎所有組織都會將此動作當做其網頁SDK實施的一部分。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Rules]**，然後選取所需的規則。
1. 在[!UICONTROL Actions]下，選取現有動作或建立動作。
1. 將[!UICONTROL Extension]下拉式欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然後將[!UICONTROL Action type]設為&#x200B;**[!UICONTROL Send event]**。

## 一般欄位

![Experience Platform Tags UI影像顯示[傳送事件]動作型別的執行個體設定。](../assets/instance-settings.png)

* **[!UICONTROL Instance]**：動作套用的SDK執行個體。 如果您的實作使用單一SDK例項，此下拉式功能表會停用。
* **[!UICONTROL Use guided events]**：啟用此選項以自動填寫或隱藏特定欄位，以啟用特定使用案例。 此設定可協助您在針對各個目的設定動作時，降低可用選項的雜訊，並遵循Adobe的最佳作法[上/下頁事件](/help/collection/use-cases/personalization/top-bottom-page-events.md)。 啟用此核取方塊會觸發下列選項按鈕的顯示：
   * **[!UICONTROL Request personalization]**：取得最新的個人化決定，而不錄製Adobe Analytics事件。 這通常稱為頁面頂端。 選取時，此選項按鈕會設定下列欄位：
      * [!UICONTROL Type]已鎖定至[!UICONTROL Decisioning Proposition Fetch]
      * [!UICONTROL Render visual personalization decisions]已鎖定以啟用
      * [!UICONTROL Automatically send a display event]已鎖定為停用
   * **[!UICONTROL Collect analytics]**：記錄事件而不取得個人化決定。 最常在頁面底部呼叫。 選取時，此選項按鈕會設定下列欄位：
      * [!UICONTROL Include rendered propositions]已鎖定以啟用

## 資料欄位

![Experience Platform Tags UI影像顯示「傳送事件」動作型別的資料元素設定。](../assets/data.png)

* **[!UICONTROL Type]**：事件型別。 您可以從預先定義的值集中選取，或定義您自己的值。 如需詳細資訊，請參閱[的`eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)接受值。 與此欄位等同的JavaScript資料庫為[`eventType`](/help/collection/js/commands/sendevent/eventtype.md)。
* **[!UICONTROL XDM]**：您要傳送至Adobe的XDM裝載。 您可以在此欄位中使用[XDM物件](../data-element-types.md#xdm-object)或[變數](../data-element-types.md#variable)。 如果您有填入多個XDM物件的規則，可以使用[合併的物件](../../core/overview.md#merged-objects)來合併它們。
* **[!UICONTROL Data]**：您要傳送至Adobe的資料裝載。 有些應用程式和服務不需要遵守XDM結構描述，例如Adobe Analytics或Adobe Target。 在此欄位中使用[變數](../data-element-types.md#variable)資料元素型別。
* **[!UICONTROL Include rendered propositions]**：啟用此核取方塊可將此事件當做顯示事件使用，包括未核取「自動傳送顯示事件」時呈現的主張。 `_experience.decisioning` XDM欄位會填入有關演算後個人化的資訊。
* **[!UICONTROL Document will unload]**：啟用此核取方塊，確保事件會到達伺服器，即使使用者離開頁面進行導覽。 此設定可讓事件連線至伺服器，但會忽略來自Edge Network的回應。
* **[!UICONTROL Merge ID]** _（已棄用）_：填入`eventMergeId` XDM欄位。

## 個人化欄位

![Experience Platform Tags UI影像顯示「傳送事件」動作型別的Personalization設定。](../assets/personalization-settings.png)

* **[!UICONTROL Scopes]**：您想要從個人化明確要求的一系列範圍。 您可以手動輸入範圍，或提供資料元素。 手動輸入範圍時，每個欄位代表一個範圍。 選取&#x200B;**[!UICONTROL Add scope]**&#x200B;以新增更多範圍至動作。
* **[!UICONTROL Surfaces]**：要查詢事件的表面陣列。 如需詳細資訊，請參閱Adobe Journey Optimizer檔案中的[建立網站體驗](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)。 手動輸入曲面時，每個欄位代表一個曲面。 選取&#x200B;**[!UICONTROL Add surface]**&#x200B;以新增更多表面至動作。
* **呈現視覺個人化決定：**&#x200B;啟用時，此核取方塊可讓您在頁面上呈現個人化內容。 如需詳細資訊，請參閱[呈現個人化內容](/help/collection/use-cases/personalization/rendering-personalization-content.md#automatically-rendering-content)。
* **[!UICONTROL Request default personalization]**：控制是否要求全頁範圍與預設表面。 預設會在頁面載入的前`sendEvent`個呼叫期間自動要求它。 與這些選項按鈕等同的JavaScript資料庫為[`requestDefaultPersonalization`](/help/collection/js/commands/sendevent/personalization.md)。 您可以從下列選項中選擇：
   * **[!UICONTROL Automatic]**：預設行為。 只有在尚未要求預設個人化時，才會要求此專案。
   * **[!UICONTROL Enabled]**：明確要求頁面範圍和預設表面。 這會更新SPA檢視快取。
   * **[!UICONTROL Disabled]**：明確隱藏頁面範圍與預設表面的要求。
* **[!UICONTROL Decision context]**：在評估裝置上決策的Adobe Journey Optimizer規則集時使用的機碼值對應。 您可以手動或透過資料元素提供決定內容。

## Advertising欄位

![Experience Platform標籤UI顯示「傳送」事件動作的廣告設定](../assets/send-event-advertising.png)

* **[!UICONTROL Request default advertising data]**：決定資料庫何時或是否將廣告資訊新增至XDM裝載。 您可以從下列選項中選擇：
   * **[!UICONTROL Automatic]**：將事件發生時可用的任何廣告資料新增至事件裝載。
   * **[!UICONTROL Wait]**：延遲傳送事件，直到收到廣告資料為止。
   * **[!UICONTROL Disabled]**：請勿將廣告資料新增至事件裝載。 如果您的實作未使用Adobe Analytics或Customer Journey Analytics，請選取此選項。

## 資料流設定覆寫

這個命令支援資料流設定覆寫，可讓您控制哪些應用程式和服務接收此資料。 當您在個別命令和標籤延伸組態設定中設定資料流組態覆寫時，個別命令優先。 如需詳細資訊，請參閱[資料流組態覆寫](../configure/configuration-overrides.md)。
