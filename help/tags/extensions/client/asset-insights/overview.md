---
title: AEM Asset Insights擴充功能概觀
description: 了解Adobe Experience Platform中的AEM Asset Insights標籤擴充功能。
exl-id: 7d3edd42-09fe-4e40-93dc-1edd2fdbb121
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 79%

---

# AEM Asset Insights擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

此擴充功能旨在搭配 [AEM Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) 共同使用。更具體來說，這將會取代「pageTracker」處理程序和內嵌程式碼。完成設定後，此擴充功能會將 Asset 的&#x200B;*「曝光數」*&#x200B;和&#x200B;*「點擊次數」*&#x200B;量度傳送至 Adobe Analytics，再由系統匯入 AEM Asset Insights 報表。之後，您就可以使用 AEM Asset Insights 或 Adobe Analytics 專案工作區查看 Asset 量度的相關報表。

## 擴充功能必備條件

### Analytics

Analytics 中的 AEM Asset 報表包含三個 AEM 維度：

* 資產 ID
* 資產來源
* 已點擊資產

此外還有兩個量度：
* 資產曝光數
* 資產點擊次數

必須使用Analytics管理員來啟用這些報表(選取 **[!UICONTROL Analytics] > [!UICONTROL 管理] > [!UICONTROL 報表套裝] > `<report suite>` > [!UICONTROL 編輯設定] > [!UICONTROL AEM] > [!UICONTROL AEM Assets報表]**)，才能使用此擴充功能填入。

「*Adobe Analytics*「 Adobe Experience Platform的標籤擴充功能必須安裝至相同的Web屬性。

### Adobe Experience Manager (AEM)

1. 啟用 [AEM Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)。在AEM中，選取 **[!UICONTROL 工具>資產]**，然後開啟 **[!UICONTROL 前瞻分析設定]** 中。

1. 停用 UUID 追蹤功能。

   >[!IMPORTANT]
   >
   >此擴充功能將 *not* 函式(若AEM Asset組態設定) **[!UICONTROL 停用UUID追蹤功能]** 已勾選。 這項設定預設為未勾選。

   ![停用 UUID 追蹤功能](images/disableassets.jpg)

## 設定 Adobe Experience Manager (AEM)

本節說明如何在Adobe Experience Platform中使用標籤設定AEM、如何在AEM中啟用Asset Insight，以及如何為資產啟用UUID追蹤功能。

### 將AEM與標籤整合

建議您透過 Adobe I/O 將 [Platform ](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html) 與 Adobe Experience Manager 整合。

1. [使用AEM連線Adobe I/O與標籤](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

2. [建立Adobe Experience PlatformCloud Service設定](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/create-launch-cloud-service.html).

### 在 AEM 中啟用 Asset Insight

如需啟用 Asset Insights 的相關說明，請參閱 [Experience Manager 6.5 資產使用手冊](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)。

### 啟用資產的 UUID 追蹤功能

在 AEM 中使用資產的 UUID，追蹤 Analytics 資產。

若要啟用資產的 UUID 追蹤功能，請開啟可編輯範本的元件原則主控台，並取消勾選「停用 UUID 追蹤」屬性(此屬性在 OOTB 影像元件預設為勾選)。

![](images/uuid.png)

啟用 UUID 後，您應該就會看見資產的 UUID 已填入「data-asset-id」資料元素。Analytics 會使用此 UUID 追蹤資產的點擊次數或曝光數。

![](images/uuid-code.png)

## 擴充功能用途

此擴充功能主要關照兩個事件和一個動作。

* **已點擊資產：**&#x200B;訪客選取已啟用追蹤功能且具有目的地 (href 屬性) 的 AEM 資產時，便會觸發此&#x200B;_事件_。

* **已點擊資產 (無目的地)：**&#x200B;訪客選取已啟用追蹤功能但無目的地 (無 href 屬性) 的 AEM 資產時，便會觸發此&#x200B;_事件_。

* **設定 AA 變數：**&#x200B;此&#x200B;_動作_&#x200B;會根據所使用的事件以及事件和動作的設定方式，設定專為 AEM Assets 保留的 Analytics 變數 (內容資料變數 `a.assets.source`、`a.assets.idlist` 和 `a.asset.clickedid`)。此擴充功能未使用任何 Analytics 事件、屬性或 eVar。

### 資產曝光數

將「設定AA變數」動作新增至新的或現有的標籤規則，此規則會在每個頁面上觸發，並傳送Analytics影像要求。 「設定 AA 變數」動作必須在「Adobe Analytics - 傳送信標」動作&#x200B;**之前**&#x200B;出現。您可視需求新增其他動作。

在&#x200B;**[「設定 AA 變數」]**&#x200B;設定頁面中，選取&#x200B;**[「已檢視資產」]** (預設) 選項。這只會針對訪客實際檢視的資產設定「曝光數」事件。

>[!NOTE]
>
>雖然不建議使用，但「設定 AA 變數」動作也支援「已載入」選項，此選項會傳送頁面上每個資產的資產曝光數 (無論訪客是否看見)。

![曝光數](images/sendImpressions.jpg)


### 資產點擊次數

使用「已點擊資產」事件和「設定 AA 變數」動作，設定第二個規則。應設定「已點擊資產」事件，將「已點擊資產影像要求」設為「頁面載入時」(預設值)。此規則不需搭配使用任何 Adobe Analytics 動作 (例如「傳送信標」)，因為資產 ID 會儲存在 `sessionStorage`，由後續的「曝光數」規則傳送。

「已點擊資產」事件也支援「點擊時」的「已點擊資產影像要求」設定。此設定會立即將點擊次數量度傳送至 Analytics，並要求 Analytics 觸發「傳送信標」動作。

![頁面載入時的資產點擊次數](images/sendClickOnPageload.jpg)

設定第三個規則，當頁面上出現無目的地 (無 `href` 屬性) 的資產時，即觸發此規則。新規則至少需搭配使用「已點擊資產 (無目的地)」事件，以及「設定 AA 變數」和「Adobe Analytics - 傳送信標」動作。您可視需要新增其他條件和動作。

![無目的地資產點擊次數](images/sendClickOnClickNoDestination.jpg)

### 擴充功能測試提示

依上述內容設定三個規則：

* 資產曝光數
* 資產點擊次數
* 無目的地資產點擊次數

**曝光數**

1. 導覽至內含 AEM 資產的頁面。

1. 如果瀏覽器未顯示資產，請適度捲動視窗，讓畫面顯示至少一個資產，接著選取所需的資產，或直接導覽至其他頁面。

1. 查看 Analytics 影像要求。

   如果 `a.assets.idlist` 含有上一頁所顯示的資產 ID，表示規則正確運作。

   如果影像要求中沒有 `a.assets.idlist`，很可能是出於下列兩個原因：

   * 瀏覽器的檢視區從未出現任何資產

   * 頁面上的資產均未透過 AEM 啟用 [Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)。

**點擊次數**

1. 導覽至內含 AEM 資產的頁面。

1. 選取任何一項資產。

如果在系統產生的 Analytics 影像要求中 (顯示於下一頁)，`a.assets.idlist` 含有目的地頁面上顯示的資產 ID，且 `a.assets.clickedid` 列出訪客在原頁面上所選取資產的資產 ID，表示規則正確運作。

如果影像要求中沒有 `a.assets.clickedid`，很可能是因為訪客選取的資產未在 AEM 中啟用 [Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)。

**無目的地的點擊次數**

1. 導覽到至少有一個無目的地 (無 `href` 屬性) AEM 資產的頁面。

1. 選取該資產。

在產生的 Analytics 影像要求中，如果 `a.assets.clickedid` 內有資產 ID，表示規則正確運作。

如果影像要求中沒有 `a.assets.clickedid`，很可能是因為訪客選取的資產未在 AEM 中啟用 [Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)。
