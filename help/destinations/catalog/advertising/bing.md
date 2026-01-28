---
keywords: 廣告；bing；
title: Microsoft Bing連線
description: 透過Microsoft Bing連線目的地，您可以在整個Microsoft Advertising網路（包括顯示廣告、搜尋和原生）中執行重新定位以及以對象為目標的數位行銷活動。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: da9ac560f65c8e0fd6c84517a47cd7e4dd868117
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 5%

---

# [!DNL Microsoft Bing] 連線 {#bing-destination}

## 概觀 {#overview}


>[!IMPORTANT]
>
>從2025年8月內部升級至目的地服務後，您的資料流中啟用的設定檔數目&#x200B;**可能會減少至**。[!DNL Microsoft Bing]
>
> 這個下降是由於針對這個目的地平台的所有啟用引入&#x200B;**ECID對應需求**&#x200B;所造成。 如需詳細資訊，請參閱此頁面中的[必要對應](#mandatory-mappings)區段。
>
>**變更內容：**
>
>* ECID (Experience Cloud ID)對應現在是所有設定檔啟用的&#x200B;**必要**。
>* 沒有ECID對應的設定檔將會從現有的啟用資料流中&#x200B;**捨棄**。
>
>**您需要執行的動作：**
>
>* 檢閱您的對象資料，以確認設定檔具有有效的ECID值。
>* 監視您的啟用量度，以驗證預期的設定檔計數。

使用[!DNL Microsoft Bing]目的地將設定檔資料傳送至整個[!DNL Microsoft Advertising Network]，包括[!DNL Display Advertising]、[!DNL Search]和[!DNL Native]。

[!DNL Microsoft Bing]目的地會在Microsoft中建立&#x200B;*[!DNL Custom Audiences]*。 如[!DNL Microsoft Search Network]Microsoft Advertising檔案[!DNL Audience Network]所列，這些在[!DNL Native]和[!DNL Display] ([!DNL Programmatic] /[ /](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500))中均可用。

若要將設定檔資料傳送至[!DNL Microsoft Bing]，您必須先連線至目的地。

## 使用案例 {#use-cases}

身為行銷人員，我想要能夠使用以[!DNL Microsoft Advertising IDs]為基礎建立的對象，透過[!DNL Microsoft Advertising]管道的顯示或搜尋廣告來鎖定使用者。

## 支援的身分 {#supported-identities}

[!DNL Microsoft Bing]支援根據下表所示的身分啟用對象。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 身分識別 | 說明 |
|---|---|
| MAID | MICROSOFT ADVERTISING ID |
| ECID | Experience Cloud ID。 此身分是整合正常運作的必要條件，但不會用於對象啟用。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

**[!DNL Audience Export]** — 您正在將對象的所有成員匯出至[!DNL Microsoft Bing]目的地。

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL Audience export]** | 您正在將對象的所有成員匯出至[!DNL Microsoft Bing]目的地。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您想要使用[!DNL Microsoft Bing]建立您的第一個目的地，而且過去尚未在Experience Cloud ID服務(使用Adobe Audience Manager或其他應用程式)中啟用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請聯絡Adobe Consulting或客戶服務以啟用ID同步。 如果您先前在Audience Manager中設定[!DNL Microsoft Bing]整合，您設定的ID同步會移轉到Experience Platform。

設定目的地時，您必須提供下列資訊：

* [!UICONTROL Account ID]：這是您的[!DNL Bing Ads CID]，以整數格式。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 填寫目標詳細資料 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL Name]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Account ID]**：您的[!DNL Bing Ads Customer ID] (CID)。 您的CID是整數，在您登入[!DNL Microsoft Advertising]時可在URL中找到。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="對應 ID"
>abstract="輸入要對應選取區段的數值 Bing 對象 ID。如果提供的[!UICONTROL Mapping ID]未對應至Bing目的地中的受眾ID，您不會在Bing帳戶中看到預期的受眾資料。"

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_bing"
>title="預先設定的對應集"
>abstract="我們已為您預先設定這兩個對應集。 當您啟用資料至Microsoft Bing時，符合啟用對象資格的設定檔必須至少有一個與其設定檔相關聯的ECID身分識別，才能成功匯出至目的地。 深入瞭解&lt;a href=&quot;https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/bing#preconfigured-mappings&quot;>預先設定的對應</a>"

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

在[對象排程](../../ui/activate-segment-streaming-destinations.md#scheduling)步驟中，您必須在[!UICONTROL Mapping ID]欄位中手動對應對象名稱。 這可確保對象中繼資料正確傳遞至[!DNL Bing]。

![顯示對象排程畫面的UI影像，其中包含如何將對象名稱對應至Bing對應ID的範例。](../../assets/catalog/advertising/bing/mapping-id.png)

### 強制對應 {#mandatory-mappings}

[支援的身分](#supported-identities)區段中說明的所有目標身分都是強制性的，必須在對象啟用程式期間進行對應。 其中包括：

* **MAID** (Microsoft Advertising ID)
* **ECID** (Experience Cloud ID)

無法對應所有必要的身分，導致您無法完成啟動工作流程。 每個身分在整合中都有不同的用途，而目的地若要正常運作，則全部為必填。

## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出至[!DNL Microsoft Bing]目的地，請檢查您的[!DNL Microsoft Bing Ads]帳戶。 如果成功啟用，系統會將對象填入您的帳戶。
