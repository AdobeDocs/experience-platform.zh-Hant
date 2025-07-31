---
keywords: 廣告；營業部；廣告營業部
title: 交易台連線
description: Trade Desk是廣告買方適用的自助式平台，可在各種顯示、影片和行動詳細目錄來源中執行重新定位以及以對象為目標的數位行銷活動。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 0954b5f22d609b0b12352de70f6c618cc88757c8
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 4%

---

# [!DNL The Trade Desk] 連線

## 概觀 {#overview}

>[!IMPORTANT]
>
>* 自2025年7月31日起，您可以在目的地目錄中並排看到兩張&#x200B;**[!DNL The Trade Desk]**&#x200B;卡片。 這是因為目標服務內部升級所致。現有的&#x200B;**[!DNL The Trade Desk]**&#x200B;目的地聯結器已重新命名為&#x200B;**[!UICONTROL （已棄用）交易台]**&#x200B;以及名稱為&#x200B;**[!UICONTROL 交易台]**&#x200B;的新卡片現在可供您使用。
>* 使用目錄中的新&#x200B;**[!UICONTROL 交易台]**&#x200B;連線，以取得新的啟用資料流程。 如果您有任何使用中的資料流至&#x200B;**[!UICONTROL （已棄用）交易台]**&#x200B;目的地，資料流會自動更新，因此您不需要採取任何動作。
>* 如果您是透過[流程服務API](https://developer.adobe.com/experience-platform-apis/references/destinations/)建立資料流，您必須將[!DNL flow spec ID]和[!DNL connection spec ID]更新為下列值：
>   * 流程規格 ID：`86134ea1-b014-49e8-8bd3-689f4ce70578`
>   * 連線規格 ID：`1029798b-a97f-4c21-81b2-e0301471166e`

使用此目的地聯結器將設定檔資料傳送至[!DNL The Trade Desk]。 此聯結器會將資料傳送至[!DNL The Trade Desk]第一方端點。 Adobe Experience Platform與[!DNL The Trade Desk]之間的整合不支援匯出資料至[!DNL The Trade Desk]第三方端點。

[!DNL The Trade Desk]是廣告購買者的自助服務平台，可在各種顯示、影片和行動詳細目錄來源中執行重新定位以及以對象為目標的數位行銷活動。

若要將設定檔資料傳送至[!DNL The Trade Desk]，您必須先連線至目的地，如本頁面的下列章節所述。

## 使用案例 {#use-cases}

身為行銷人員，我想要能夠使用以[!DNL Trade Desk IDs]或裝置ID建立的對象來建立重新定位或以對象為目標的數位行銷活動。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk]支援根據下表所示的身分啟用對象。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

以下是[!DNL The Trade Desk]目的地支援的身分。 這些身分識別可用來啟動[!DNL The Trade Desk]的對象。

下表中的所有身分都是強制對應。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |
| ECID | Experience Cloud ID | 此身分是整合正常運作的必要條件，但不會用於對象啟用。 |
| 交易台ID | [!DNL The Trade Desk]平台中的廣告商ID | 根據Trade Desk的專屬ID啟用對象時，請使用此身分識別。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在將對象的所有成員匯出至目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您想要使用[!DNL The Trade Desk]建立您的第一個目的地，而且過去尚未在Experience Cloud ID服務(使用Adobe Audience Manager或其他應用程式)中啟用[ID同步功能](https://experienceleague.adobe.com/zh-hant/docs/id-service/using/id-service-api/methods/idsync)，請聯絡Adobe Consulting或客戶服務以啟用ID同步。 如果您先前在Audience Manager中設定[!DNL The Trade Desk]整合，您設定的ID同步會移轉到Experience Platform。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 帳戶識別碼]**：您的[!DNL The Trade Desk] [!UICONTROL 帳戶識別碼]。
* **[!UICONTROL 伺服器位置]**：請詢問您的[!DNL The Trade Desk]代表您應該使用哪個區域伺服器。 以下是您可選擇使用的地區伺服器：

   * **[!UICONTROL APAC]**
   * **[!UICONTROL 中國]**
   * **[!UICONTROL 東京]**
   * **[!UICONTROL 英國/歐盟]**
   * **[!UICONTROL 美國東岸]**
   * **[!UICONTROL 美國西海岸]**

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

在[對象排程](../../ui/activate-segment-streaming-destinations.md#scheduling)步驟中，您必須手動將對象對應至目的地平台中其對應的ID或易記名稱。

對應對象時，Adobe建議您使用Experience Platform對象名稱或較短的形式，以方便使用。 不過，您目的地中的對象ID或名稱不需要符合Experience Platform帳戶中的對象ID。 您在對應欄位中插入的任何值都會反映在目的地中。

### 強制對應 {#mandatory-mappings}

[支援的身分](#supported-identities)區段中說明的所有目標身分都是強制性的，必須在對象啟用程式期間進行對應。 其中包括：

* **GAID** (Google Advertising ID)
* **IDFA** (廣告商的Apple ID)
* **ECID** (Experience Cloud ID)
* **交易台ID**

如果無法對應所有必要的身分，將無法成功將對象啟用至[!DNL The Trade Desk]。 每個身分在整合中都有不同的用途，而目的地若要正常運作，則全部為必填。

![顯示必要對應的熒幕擷圖](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出至[!DNL The Trade Desk]目的地，請檢查您的[!DNL The Trade Desk]帳戶。 如果成功啟用，系統會將對象填入您的帳戶。
