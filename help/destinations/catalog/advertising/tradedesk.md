---
keywords: 廣告；營業部；廣告營業部
title: 交易台連線
description: Trade Desk是廣告買方適用的自助式平台，可在各種顯示、影片和行動詳細目錄來源中執行重新定位以及以對象為目標的數位行銷活動。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 4%

---

# [!DNL The Trade Desk] 連線

## 概觀 {#overview}

使用此目的地聯結器將設定檔資料傳送至[!DNL The Trade Desk]。 此聯結器會將資料傳送至[!DNL The Trade Desk]第一方端點。 Adobe Experience Platform與[!DNL The Trade Desk]之間的整合不支援匯出資料至[!DNL The Trade Desk]第三方端點。

[!DNL The Trade Desk]是廣告購買者的自助服務平台，可在各種顯示、影片和行動詳細目錄來源中執行重新定位以及以對象為目標的數位行銷活動。

若要將設定檔資料傳送至[!DNL The Trade Desk]，您必須先連線至目的地，如本頁面的下列章節所述。

## 使用案例 {#use-cases}

身為行銷人員，我想要能夠使用以[!DNL Trade Desk IDs]或裝置ID建立的對象來建立重新定位或以對象為目標的數位行銷活動。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk]支援根據下表所示的身分啟用對象。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

以下是[!DNL The Trade Desk]目的地支援的身分。 這些身分識別可用來啟動[!DNL The Trade Desk]的對象。

下表中的所有身分都已預先設定，並在啟用期間自動對應。 您不需要在啟動工作流程中手動設定這些對應。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 當GAID出現在設定檔上時啟用。 |
| IDFA | 廣告商適用的Apple ID | 當IDFA存在於設定檔上時啟動。 |
| ECID | Experience Cloud ID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 如需詳細資訊，請參閱[ECID](/help/identity-service/features/ecid.md)上的下列檔案。 |
| [!DNL Tradedesk] | [!DNL TDID]平台中的[!DNL The Trade Desk] | 當設定檔具有ECID，且Experience Platform中存在ECID對交易台ID對應時啟用。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 所有其他受眾來源 | 是 | 此類別包含透過[!DNL Segmentation Service]產生的對象以外的所有對象來源。 閱讀[各種對象來源](/help/segmentation/ui/audience-portal.md#customize)。 部分範例包括： <ul><li> 自訂上傳對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform，</li><li> 相似受眾， </li><li> 同盟對象， </li><li> 在其他Experience Platform應用程式(例如Adobe Journey Optimizer)中產生的對象， </li><li> 及更多內容。 </li></ul> |

{style="table-layout:auto"}



依受眾資料型別支援的受眾：

| 對象資料型別 | 支援 | 說明 | 使用案例 |
|--------------------|-----------|-------------|-----------|
| [人員對象](/help/segmentation/types/people-audiences.md) | 是 | 根據客戶設定檔，可讓您針對行銷活動的特定人群進行定位。 | 經常購買者、購物車放棄者 |
| [帳戶對象](/help/segmentation/types/account-audiences.md) | 無 | 針對帳戶型行銷策略，鎖定特定組織內的個人。 | B2B行銷 |
| [潛在客戶對象](/help/segmentation/types/prospect-audiences.md) | 無 | 將目標定位為尚未成為客戶但與目標受眾具有相同特性的個人。 | 使用第三方資料進行勘探 |
| [資料集匯出](/help/catalog/datasets/overview.md) | 無 | 儲存在Adobe Experience Platform Data Lake中的結構化資料集合。 | 報告、資料科學工作流程 |

{style="table-layout:auto"}


## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL Audience export]** | 您正在將對象的所有成員匯出至目的地。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

先決條件取決於您計畫用於對象啟用的身分型別：

**僅針對行動識別碼啟用**，沒有先決條件。 只要您收集並管理客戶的ID （GAID及/或IDFA），您就可以開始將受眾啟用至[!DNL The Trade Desk]。

**針對[!DNL The Trade Desk]**&#x200B;上的Cookie型鎖定目標，請確定已在ECID與[!DNL Trade Desk ID]之間建立對應。 請完成下列步驟以執行此操作：

1. **啟用ID同步功能**：如果您是第一次設定[!DNL The Trade Desk ID]啟用，而且您過去尚未在Experience Cloud ID服務中啟用[ID同步功能](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/idsync) (使用Adobe Audience Manager或其他應用程式)，請聯絡Adobe Consulting或客戶服務以啟用ID同步。
   * 如果您先前在Audience Manager中設定[!DNL The Trade Desk]整合，您現有的ID同步會自動傳遞至Experience Platform。

2. **檢測您的網頁**：在您的網頁上實作程式碼，以建立[!DNL The Trade Desk ID]與Adobe ECID之間的對應。 這可讓Experience Platform將交易台ID與您的客戶設定檔建立關聯。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL Name]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Account ID]**：您的[!DNL The Trade Desk] [!UICONTROL Account ID]。
* **[!UICONTROL Server Location]**：請詢問您的[!DNL The Trade Desk]代表您應該使用哪個地區伺服器。 以下是您可選擇使用的地區伺服器：

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL UK/EU]**
   * **[!UICONTROL US East Coast]**
   * **[!UICONTROL US West Coast]**

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

在[對象排程](../../ui/activate-segment-streaming-destinations.md#scheduling)步驟中，您必須手動將對象對應至目的地平台中其對應的ID或易記名稱。

對應對象時，Adobe建議您使用Experience Platform對象名稱或較短的形式，以方便使用。 不過，您目的地中的對象ID或名稱不需要符合Experience Platform帳戶中的對象ID。 您在對應欄位中插入的任何值都會反映在目的地中。

### 預先設定的對應 {#preconfigured-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="預先設定的對應集"
>abstract="我們已為您預先設定這四個對應集。當您向交易台啟用資料時，符合啟用對象資格的設定檔不一定要在設定檔上呈現所有四個身分，因為此目的地將可搭配此處顯示的任何目標身分使用。 <br>若要根據交易台ID進行Cookie型鎖定目標，您需要出現在設定檔上的ECID，以及交易台ID與ECID之間的ID同步對應。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-platform/destinations/catalog/advertising/tradedesk#preconfigured-mappings" text="深入了解預先設定的對應"

下列身分對應已預先設定&#x200B;**並在對象啟用工作流程中自動為您填入**：

* GAID (Google Advertising ID)
* IDFA (廣告商的Apple ID)
* ECID (Experience Cloud ID)
* [!DNL The Trade Desk ID]

![顯示必要對應的熒幕擷圖](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

這些對應會呈現灰色，而且是唯讀的。 您不需要在此步驟中設定任何專案。 選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

Experience Platform會自動檢查屬於啟用工作流程中對應之對象的每個設定檔，以取得所有支援的身分型別，然後使用出現的任何身分啟用設定檔。

### 依啟用型別區分的身分需求

**行動ID啟用(GAID/IDFA)：**&#x200B;只包含GAID或IDFA的設定檔就足以啟用。 不需要其他身分或先決條件。

**Cookie型鎖定目標([!DNL Trade Desk ID])：**&#x200B;需要兩者：

* 設定檔上存在ECID
* [!DNL Trade Desk ID]與ECID之間的ID同步對應（如[必要條件](#prerequisites)一節中所述進行設定）

**多個ID行為：**&#x200B;如果設定檔包含多個支援的身分，則每個身分將分別啟動至[!DNL The Trade Desk]。 這可確保您的受眾啟動具有最大的觸及率和彈性。

### 啟用範例

* **行動ID設定檔：**&#x200B;具有GAID和/或IDFA的設定檔已使用各自的廣告ID啟用。 如果設定檔同時包含GAID和IDFA，則每個ID將分別啟動。
* **以Cookie為基礎的設定檔：**&#x200B;將使用Trade Desk ID來啟動具有ECID與對應[!DNL Trade Desk ID]對應的設定檔，以進行Cookie型目標定位。
* **僅限ECID的設定檔：**&#x200B;僅具有ECID且沒有[!DNL Trade Desk ID]對應的設定檔&#x200B;**將不會匯出**。 ECID本身不足以啟動。

## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出至[!DNL The Trade Desk]目的地，請檢查您的[!DNL The Trade Desk]帳戶。 如果成功啟用，系統會將對象填入您的帳戶。
