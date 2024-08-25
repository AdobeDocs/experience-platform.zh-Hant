---
keywords: 廣告；bing；
title: Microsoft Bing連線
description: 透過Microsoft Bing連線目的地，您可以在整個Microsoft Advertising網路（包括顯示廣告、搜尋和原生）中執行重新定位以及以對象為目標的數位行銷活動。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 10%

---

# [!DNL Microsoft Bing]個連線 {#bing-destination}

## 概觀 {#overview}

使用[!DNL Microsoft Bing]目的地將設定檔資料傳送至整個[!DNL Microsoft Advertising Network]，包括[!DNL Display Advertising]、[!DNL Search]和[!DNL Native]。

[!DNL Microsoft Bing]目的地會在Microsoft中建立&#x200B;*[!DNL Custom Audiences]*。 如[Microsoft Advertising檔案](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500)所列，這些在[!DNL Microsoft Search Network]和[!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic])中均可用。

若要將設定檔資料傳送至[!DNL Microsoft Bing]，您必須先連線至目的地。

## 使用案例 {#use-cases}

身為行銷人員，我想要能夠使用以[!DNL Microsoft Advertising IDs]為基礎建立的對象，透過[!DNL Microsoft Advertising]管道的顯示或搜尋廣告來鎖定使用者。

## 支援的身分 {#supported-identities}

[!DNL Microsoft Bing]支援根據下表所示的身分啟用對象。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 身分 | 說明 |
|---|---|
| MAID | MICROSOFT ADVERTISING ID |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform[細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ (A) | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

**[!DNL Audience Export]** — 您正在將對象的所有成員匯出至[!DNL Microsoft Bing]目的地。

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在將對象的所有成員匯出至[!DNL Microsoft Bing]目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您想要使用[!DNL Microsoft Bing]建立您的第一個目的地，而且先前未在Experience CloudID服務(使用Adobe Audience Manager或其他應用程式)中啟用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請聯絡Adobe Consulting或客戶服務以啟用ID同步。 如果您先前在Audience Manager中設定[!DNL Microsoft Bing]整合，則您設定的ID同步會移轉到Platform。

設定目的地時，您必須提供下列資訊：

* [!UICONTROL 帳戶ID]：這是您的[!DNL Bing Ads CID]，以整數格式。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 填寫目標詳細資訊 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 帳戶識別碼]**：您的[!DNL Bing Ads Customer ID] (CID)。 您的CID是整數，在您登入[!DNL Microsoft Advertising]時可在URL中找到。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的客群 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="對應 ID"
>abstract="輸入要對應選取區段的數值 Bing 客群 ID。如果提供的[!UICONTROL 已對應 ID] 未對應至 Bing 目的地中的客群 ID，您將不會在 Bing 帳戶中看到預期的客群資料。"

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

在[對象排程](../../ui/activate-segment-streaming-destinations.md#scheduling)步驟中，您必須在[!UICONTROL 對應ID]欄位中手動對應對象名稱。 這可確保對象中繼資料正確傳遞至[!DNL Bing]。

![顯示對象排程畫面的UI影像，其中包含如何將對象名稱對應至Bing對應ID的範例。](../../assets/catalog/advertising/bing/mapping-id.png)

## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出至[!DNL Microsoft Bing]目的地，請檢查您的[!DNL Microsoft Bing Ads]帳戶。 如果成功啟用，系統會將對象填入您的帳戶。
