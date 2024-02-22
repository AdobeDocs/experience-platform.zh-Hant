---
title: Google顯示和視訊360連線
description: Display & Video 360 （先前稱為DoubleClick Bid Manager）工具可用來跨顯示器、影片和行動庫存來源執行重新定位以及以對象為目標的數位行銷活動。
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: d5a22d4692226c865f6489c821366b4ce8bc2887
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] 連線

>[!IMPORTANT]
>
> Google即將發佈的變更專案 [Google Ads API](https://developers.google.com/google-ads/api/docs/start)， [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)，以及 [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) 以支援「 」中定義的合規性和同意相關要求 [數位市場法案](https://digital-markets-act.ec.europa.eu/index_en) (DMA)在歐盟([歐盟使用者同意原則](https://www.google.com/about/company/user-consent-policy/))。 預計這些同意要求變更將於2024年3月6日起生效。
><br/><br/>
>為了遵循歐盟使用者同意政策並繼續為歐洲經濟區(EEA)的使用者建立對象清單，廣告商和合作夥伴必須確保在上傳對象資料時傳遞一般使用者同意。 Adobe身為Google合作夥伴，為您提供在歐盟DMA下符合這些同意要求的必要工具。
><br/><br/>
>已購買AdobePrivacy &amp; Security Shield且已設定 [同意原則](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 不需要採取任何動作，即可篩選出未同意的設定檔。
><br/><br/>
>尚未購買AdobePrivacy &amp; Security Shield的客戶必須使用 [區段定義](../../../segmentation/home.md#segment-definitions) 中的功能 [區段產生器](../../../segmentation/ui/segment-builder.md) 以篩選掉未同意的設定檔，以便持續使用現有的Real-Time CDP Google目標而不中斷。

[!DNL Display & Video 360]，先前稱為 [!DNL DoubleClick Bid Manager]，是用於跨顯示、影片和行動詳細目錄來源執行重新定位以及以對象為目標的數位行銷活動的工具。

## 目的地詳情 {#specifics}

請注意以下專屬於您的詳細資訊 [!DNL Google Display & Video 360] 目的地：

* 啟用的對象是在Google平台中以程式設計方式建立的。
* 將受眾回填啟用至 [!DNL Google Display & Video 360] 目的地會排程在對象首次對應至目的地連線的24到48小時後發生。 此更新是為了因應Google等候24小時擷取資料的原則，並旨在改善Real-Time CDP與之間的匹配率。 [!DNL Google Display & Video 360]. 這是隻適用於此目的地的後端設定，與UI中任何可由客戶設定的排程選項無關。

>[!IMPORTANT]
>
>如果您打算使用Google Display &amp; Video 360建立您的第一個目的地，但尚未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 若是過去的Experience CloudID服務(使用Adobe Audience Manager或其他應用程式)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前在Audience Manager中設定Google整合，您設定的ID同步會延續至Platform。

## 支援的身分 {#supported-identities}

[!DNL Google Display & Video 360] 支援根據下表所示的身分來啟用對象。 進一步瞭解 [身分](/help/identity-service/features/namespaces.md).

| 身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也稱為 [!DNL Device ID]. 38位數的裝置ID，Audience Manager會與每個與其互動的裝置建立關聯。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) 以加州的目標使用者，以及所有其他使用者的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 使用此ID來鎖定加州以外的使用者。 |
| RIDA | 適用於廣告的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| MAID | Microsoft廣告ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire電視。 |  |

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在將對象的所有成員匯出至Google目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

## 先決條件 {#prerequisites}

### 允許清單 {#allow-listing}

>[!NOTE]
>
>必須先將列入允許清單，才能設定您的第一個 [!DNL Google Display & Video 360] Platform中的目的地。 請確定下列說明的允許清單程式已由完成 [!DNL Google] 建立目的地之前。
>此規則的例外情況是 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 客戶。 如果您已經在Audience Manager中建立了與此Google目的地的連線，則不需要再次進行允許清單程式，您可以繼續後續步驟。

建立之前 [!DNL Google Display & Video 360] 在Platform中的目的地，您必須聯絡Google以要求Adobe加入允許的資料提供者清單，並將您的帳戶新增至允許清單。 請聯絡Google並提供下列資訊：

* **帳戶ID**：Adobe的帳戶ID與Google。 帳戶ID：87933855。
* **客戶ID**：Adobe的客戶帳戶ID與Google。 客戶ID：89690775。
* **您的帳戶型別**：使用 **[!DNL Invite advertiser]** 只允許與您Display &amp; Video 360帳戶中的特定品牌共用對象，或使用 **[!DNL Invite partner]** 可讓您的顯示和視訊360帳戶中的所有品牌共用對象。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 說明]**：選填。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL 帳戶型別]**：根據您使用Google的帳戶，選取選項：
   * 使用 `Invite Advertiser` 僅允許將對象共用給您的Display &amp; Video 360帳戶中的特定品牌。
   * 使用 `Invite Partner` 可讓您的顯示和視訊360帳戶中的所有品牌共用對象。
* **[!UICONTROL 帳戶ID]**：填入 **[!DNL Invite partner]** 或 **[!DNL Invite advertiser]** 使用Google的帳戶ID。 通常是6或7位數的ID。

>[!NOTE]
>
>設定時 [!DNL Google Display & Video 360] 目的地，使用您的 [!DNL Google Account Manager] 或Adobe代表以瞭解您的帳戶型別。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用受眾資料至串流受眾匯出目的地](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

## 匯出的資料

驗證資料是否已成功匯出至 [!DNL Google Display & Video 360] 目的地，請檢視您的 [!DNL Google Display & Video 360] 帳戶。 如果成功啟用，系統會將對象填入您的帳戶。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤訊息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合 [必備條件](#prerequisites). 若要修正此問題，請聯絡Google並確認您的帳戶已加入允許清單。