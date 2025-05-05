---
title: Google顯示和視訊360連線
description: Display & Video 360 （先前稱為DoubleClick Bid Manager）工具可用來跨顯示器、影片和行動庫存來源執行重新定位以及以對象為目標的數位行銷活動。
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 4%

---

# [!DNL Google Display & Video 360]個連線

>[!IMPORTANT]
>
> Google正在發佈[Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)和[Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)的變更，以支援歐盟（[歐盟使用者同意政策](https://www.google.com/about/company/user-consent-policy/)）中[數位市場法](https://digital-markets-act.ec.europa.eu/index_en) (DMA)所定義的法規遵循與同意相關需求。 自2024年3月6日起，將開始強制執行同意要求的這些變更。
><br/>
>為了遵循歐盟使用者同意政策並繼續為歐洲經濟區(EEA)的使用者建立對象清單，廣告商和合作夥伴必須確保在上傳對象資料時傳遞一般使用者同意。 作為 Google 合作夥伴，Adobe 會為您提供必要的工具，以遵守歐盟之 DMA 規定的這些同意要求。
><br/>
>已購買Adobe Privacy &amp; Security Shield且已設定[同意原則](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)以篩選掉非同意的設定檔的客戶，不必採取任何動作。
><br/>
>未購買Adobe Privacy &amp; Security Shield的客戶必須使用[區段產生器](../../../segmentation/ui/segment-builder.md)中的[區段定義](../../../segmentation/home.md#segment-definitions)功能，篩選出未同意的設定檔，才能繼續使用現有的Real-Time CDP Google目的地而不中斷。

[!DNL Display & Video 360] （先前稱為[!DNL DoubleClick Bid Manager]）是用來跨顯示器、視訊和行動詳細目錄來源執行重新定位以及以對象為目標的數位行銷活動的工具。

## 目的地詳情 {#specifics}

請注意下列專屬於[!DNL Google Display & Video 360]目的地的詳細資料：

* 啟用的對象是在Google平台中以程式設計方式建立的。
* 將對象回填啟用至[!DNL Google Display & Video 360]目的地的排程，安排在對象首次對應至目的地連線的24至48小時後進行。 此更新是為了回應Google等待24小時直到擷取資料的原則，其目的是為了改善Real-Time CDP與[!DNL Google Display & Video 360]之間的匹配率。 這是隻適用於此目的地的後端設定，與UI中任何可由客戶設定的排程選項無關。

>[!IMPORTANT]
>
>如果您打算使用Google Display &amp; Video 360建立您的第一個目的地，而且過去尚未在Experience Cloud ID服務(使用Adobe Audience Manager或其他應用程式)中啟用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=zh-Hant)，請聯絡Adobe Consulting或客戶服務以啟用ID同步。 如果您先前在Audience Manager中設定Google整合，您設定的ID同步會傳遞至Experience Platform。

## 支援的身分 {#supported-identities}

[!DNL Google Display & Video 360]支援根據下表所示的身分啟用對象。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 身分識別 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hant)，也稱為[!DNL Device ID]。 Audience Manager與其互動的每個裝置相關聯的數字38位數裝置ID。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hant)來鎖定加州的使用者，並使用所有其他使用者的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google]使用此ID來鎖定加州以外的使用者。 |
| RIDA | Advertising的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| MAID | Microsoft Advertising ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire電視。 |  |

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
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在將對象的所有成員匯出至Google目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

## 先決條件 {#prerequisites}

### 允許清單 {#allow-listing}

>[!NOTE]
>
>在Experience Platform中設定第一個[!DNL Google Display & Video 360]目的地前，必須先加入允許清單。 在建立目的地之前，請確定[!DNL Google]已完成下述允許清單程式。
>此規則的例外情況適用於[Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=zh-Hant)客戶。 如果您已經在Audience Manager中建立了與此Google目的地的連線，則不需要再次進行允許清單程式，您可以繼續後續步驟。

在Experience Platform中建立[!DNL Google Display & Video 360]目的地之前，您必須聯絡Google以要求Adobe加入允許的資料提供者清單，並將您的帳戶新增至允許清單。 請聯絡Google並提供下列資訊：

* **帳戶ID**： Adobe的帳戶ID與Google。 帳戶ID：87933855。
* **客戶ID**： Adobe的客戶帳戶ID與Google。 客戶ID：89690775。
* **您的帳戶型別**：使用&#x200B;**[!DNL Invite advertiser]**&#x200B;以允許對象僅與您顯示與視訊360帳戶中的特定品牌共用，或使用&#x200B;**[!DNL Invite partner]**&#x200B;以允許對象與您顯示與視訊360帳戶中的所有品牌共用。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 描述]**：選擇性。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL 帳戶型別]**：根據您在Google中的帳戶，選取選項：
   * 使用`Invite Advertiser`可允許對象僅與您的Display &amp; Video 360帳戶中的特定品牌分享。
   * 使用`Invite Partner`可讓您的顯示與視訊360帳戶中的所有品牌共用對象。
* **[!UICONTROL 帳戶ID]**：使用Google填入您的&#x200B;**[!DNL Invite partner]**&#x200B;或&#x200B;**[!DNL Invite advertiser]**&#x200B;帳戶ID。 通常是6或7位數的ID。

>[!NOTE]
>
>設定[!DNL Google Display & Video 360]目的地時，請與您的[!DNL Google Account Manager]或Adobe代表合作，瞭解您擁有哪種帳戶型別。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

## 匯出的資料

若要確認資料是否已成功匯出至[!DNL Google Display & Video 360]目的地，請檢查您的[!DNL Google Display & Video 360]帳戶。 如果成功啟用，系統會將對象填入您的帳戶。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤訊息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合[必要條件](#prerequisites)時，就會發生此錯誤。 若要修正此問題，請聯絡Google並確認您的帳戶已加入允許清單。