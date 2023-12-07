---
keywords: 廣告；bing；
title: Microsoft Bing連線
description: 透過Microsoft Bing連線目的地，您可以在整個Microsoft Advertising網路（包括顯示廣告、搜尋和原生）中執行重新定位以及以對象為目標的數位行銷活動。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: c4169d9371d329e445db7c83820b870ccbba238b
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 10%

---

# [!DNL Microsoft Bing] 連線 {#bing-destination}

## 概觀 {#overview}

使用 [!DNL Microsoft Bing] 將設定檔資料傳送至整個的目的地 [!DNL Microsoft Advertising Network]，包括 [!DNL Display Advertising]， [!DNL Search]、和 [!DNL Native].

此 [!DNL Microsoft Bing] 目的地建立 *[!DNL Custom Audiences]* 在Microsoft中。 這些選項都可在 [!DNL Microsoft Search Network] 和 [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic])中所列的) [Microsoft Advertising檔案](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

若要傳送設定檔資料至 [!DNL Microsoft Bing]，您必須先連線至目的地。

## 使用案例 {#use-cases}

身為行銷人員，我想要能夠使用由下列專案建立的對象： [!DNL Microsoft Advertising IDs] 若要透過顯示或搜尋廣告鎖定使用者，請 [!DNL Microsoft Advertising] 管道。

## 支援的身分 {#supported-identities}

[!DNL Microsoft Bing] 支援根據下表所示的身分來啟用對象。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 身分 | 說明 |
|---|---|
| MAID | Microsoft廣告ID |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

**[!DNL Audience Export]**  — 您正在將對象的所有成員匯出至 [!DNL Microsoft Bing] 目的地。

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在將對象的所有成員匯出至 [!DNL Microsoft Bing] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您打算使用建立您的第一個目的地 [!DNL Microsoft Bing] 且尚未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 若是過去的Experience CloudID服務(使用Adobe Audience Manager或其他應用程式)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已設定 [!DNL Microsoft Bing] Audience Manager中的整合，也就是您設定的ID同步會移轉到Platform。

設定目的地時，您必須提供下列資訊：

* [!UICONTROL 帳戶ID]：這是您的 [!DNL Bing Ads CID]，以整數格式顯示。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 填寫目標詳細資訊 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**：您的 [!DNL Bing Ads Customer ID] (CID)。 您的CID是整數，可在您登入時於URL中找到 [!DNL Microsoft Advertising].

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="對應 ID"
>abstract="輸入要對應選取區段的數值 Bing 對象 ID。如果提供的[!UICONTROL 已對應 ID] 未對應至 Bing 目的地中的對象 ID，您將不會在 Bing 帳戶中看到預期的對象資料。"

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用受眾資料至串流受眾匯出目的地](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

在 [對象排程](../../ui/activate-segment-streaming-destinations.md#scheduling) 步驟，您必須手動將對象名稱對應 [!UICONTROL 對應ID] 欄位。 這可確保對象中繼資料可正確傳遞至 [!DNL Bing].

![顯示對象排程畫面的UI影像，其中包含如何將對象名稱對應至Bing對應ID的範例。](../../assets/catalog/advertising/bing/mapping-id.png)

## 匯出的資料 {#exported-data}

驗證資料是否已成功匯出至 [!DNL Microsoft Bing] 目的地，請檢視您的 [!DNL Microsoft Bing Ads] 帳戶。 如果成功啟用，系統會將對象填入您的帳戶。
