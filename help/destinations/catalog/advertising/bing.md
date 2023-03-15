---
keywords: 廣告；bing;
title: Microsoft Bing連線
description: 使用Microsoft Bing連線目的地，您可以在Microsoft Display Advertising中執行重新鎖定目標和對象鎖定目標的數位促銷活動。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: aec9708680c2a4cb3c70af12f95c67ec37b2e129
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# [!DNL Microsoft Bing] 連接 {#bing-destination}

## 總覽 {#overview}

此 [!DNL Microsoft Bing] 目的地可協助您將設定檔資料傳送至 [!DNL Microsoft Display Advertising].

若要將設定檔資料傳送至 [!DNL Microsoft Bing]，您必須先連線至目的地。

## 使用案例 {#use-cases}

身為行銷人員，我想要使用以 [!DNL Microsoft Advertising IDs] 透過 [!DNL Microsoft Advertising] 管道。

## 支援的身分 {#supported-identities}

[!DNL Microsoft Bing] 支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 |
|---|---|
| 女傭 | Microsoft Advertising ID |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

**[!DNL Segment Export]**  — 將區段（對象）的所有成員匯出至 [!DNL Microsoft Bing] 目的地。

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在將區段（對象）的所有成員匯出至 [!DNL Microsoft Bing] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您想要使用 [!DNL Microsoft Bing] 並未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 過去(使用Adobe Audience Manager或其他應用程式)的Experience CloudID服務，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您之前 [!DNL Microsoft Bing] Audience Manager中的整合，即您設定並繼承至Platform的ID同步。

設定目的地時，您必須提供下列資訊：

* [!UICONTROL 帳戶ID]:這是你的 [!DNL Bing Ads CID]，格式為整數。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的 [!DNL Bing Ads Customer ID] (CID)。 您的CID是整數，在您登入時可在URL中找到 [!DNL Microsoft Advertising].

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="對應ID"
>abstract="輸入您要對應所選區段的數值Bing區段ID。 如果提供 [!UICONTROL 對應ID] 未對應至Bing目的地的區段ID，您將無法在Bing帳戶中看到預期的對象資料。"

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

在 [區段排程](../../ui/activate-segment-streaming-destinations.md#scheduling) 步驟中，您必須手動對應 [!UICONTROL 對應ID] 欄位。 這可確保區段中繼資料正確傳遞至 [!DNL Bing].

![顯示區段排程畫面的UI影像，內含如何將區段名稱對應至Bing對應ID的範例。](../../assets/catalog/advertising/bing/mapping-id.png)

## 匯出的資料 {#exported-data}

驗證資料是否已成功導出到 [!DNL Microsoft Bing] 目的地，檢查 [!DNL Microsoft Bing Ads] 帳戶。 如果啟動成功，則會在您的帳戶中填入對象。
