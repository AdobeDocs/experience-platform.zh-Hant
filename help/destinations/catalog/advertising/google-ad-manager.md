---
keywords: google廣告管理員；google廣告；doubleclick；DoubleClick AdX；DoubleClick；Google廣告管理員；Google廣告管理員；DFP
title: Google廣告管理員連線
description: Google Ad Manager （舊稱為DoubleClick for Publishers或DoubleClick AdX）是Google的廣告服務平台，可讓發佈者透過視訊和行動應用程式管理其網站上的廣告顯示。
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 7%

---

# [!DNL Google Ad Manager]個連線

>[!IMPORTANT]
>
> Google正在發佈[Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)和[Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)的變更，以支援歐盟（[歐盟使用者同意政策](https://www.google.com/about/company/user-consent-policy/)）中[數位市場法](https://digital-markets-act.ec.europa.eu/index_en) (DMA)所定義的法規遵循與同意相關需求。 自2024年3月6日起，將開始強制執行同意要求的這些變更。
><br/>
>為了遵循歐盟使用者同意政策並繼續為歐洲經濟區(EEA)的使用者建立對象清單，廣告商和合作夥伴必須確保在上傳對象資料時傳遞一般使用者同意。 作為 Google 合作夥伴，Adobe 會為您提供必要的工具，以遵守歐盟之 DMA 規定的這些同意要求。
><br/>
>已購買Adobe Privacy &amp; Security Shield且已設定[同意原則](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)以篩選掉非同意的設定檔的客戶，不必採取任何動作。
><br/>
>未購買Adobe Privacy &amp; Security Shield的客戶必須使用[區段產生器](../../../segmentation/ui/segment-builder.md)中的[區段定義](../../../segmentation/home.md#segment-definitions)功能，篩選出未同意的設定檔，才能繼續使用現有的Real-Time CDP Google目的地而不中斷。


[!DNL Google Ad Manager] (先前稱為[!DNL DoubleClick for Publishers] (DFP)或[!DNL DoubleClick AdX])是來自[!DNL Google]的廣告服務平台，可讓發佈者透過視訊和行動應用程式管理其網站上廣告的顯示。

## 目的地詳情 {#specifics}

請注意下列專屬於[!DNL Google Ad Manager]目的地的詳細資料：

* 啟用的對象是以程式設計方式在[!DNL Google]平台中建立。
* [!DNL Platform]目前不包含驗證成功啟用的測量量度。 請參考Google中的對象計數，以驗證整合併瞭解對象目標定位大小。
* 將對象對應到[!DNL Google Ad Manager]目的地後，對象名稱會立即出現在[!DNL Google Ad Manager]使用者介面中。
* 區段母體需要24到48小時才能出現在[!DNL Google Ad Manager]中。 此外，受眾必須具有至少50個設定檔的受眾大小，才能在[!DNL Google Ad Manager]中顯示。 大小小於50個設定檔的對象將不會填入[!DNL Google Ad Manager]。

## 支援的身分 {#supported-identities}

[!DNL Google Ad Manager]支援根據下表所示的身分啟用對象。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 身分識別 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也稱為[!DNL Device ID]。 Audience Manager與其互動的每個裝置相關聯的數字38位數裝置ID。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)來鎖定加州的使用者，並使用所有其他使用者的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google]使用此ID來鎖定加州以外的使用者。 |
| RIDA | Advertising的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| MAID | Microsoft Advertising ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire電視。 |  |

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
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在將對象的所有成員匯出至Google目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

如果您想要使用[!DNL Google Ad Manager]建立您的第一個目的地，而且過去尚未在Experience Cloud ID服務(使用Audience Manager或其他應用程式)中啟用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請聯絡Adobe Consulting或客戶服務以啟用ID同步。 如果您先前在Audience Manager中設定[!DNL Google]整合，您設定的ID同步會移轉到Platform。

### 允許清單 {#allow-listing}

在Platform中設定第一個[!DNL Google Ad Manager]目的地前，必須先加入允許清單。 在建立目的地之前，請務必完成下述允許清單程式。

1. 依照[Google Ad Manager檔案](https://support.google.com/admanager/answer/3289669?hl=en)中所述的步驟，將Adobe新增為連結的資料管理平台(DMP)。
2. 在[!DNL Google Ad Manager]介面中，移至&#x200B;**[!UICONTROL 管理員]** > **[!UICONTROL 全域設定]** > **[!UICONTROL 網路設定]**，並啟用&#x200B;**[!UICONTROL API存取]**&#x200B;滑桿。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="將對象 ID 附加到對象名稱"
>abstract="選取此選項可讓 Google Ad Manager 中的對象名稱包含來自 Experience Platform 的對象 ID，如下所示：`Audience Name (Audience ID)`"

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 描述]**：選擇性。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL 帳戶識別碼]**：從您的[!DNL Google]帳戶輸入您的[!DNL Audience Link ID]。 這是與您的[!DNL Google Ad Manager]網路（不是您的[!DNL Network code]）相關聯的特定識別碼。 您可以在[!DNL Google Ad Manager]介面的&#x200B;**[!UICONTROL 管理員>全域設定]**&#x200B;下找到此專案。
* **[!UICONTROL 帳戶型別]**：根據您在Google中的帳戶，選取選項：
   * 使用`DFP by Google`作為發行者的[!DNL DoubleClick]
   * 對[!DNL Google AdX]使用`AdX buyer`
* **[!UICONTROL 將對象ID附加至對象名稱]**：選取此選項，讓Google Ad Manager中的對象名稱包含Experience Platform中的對象ID，如下所示： `Audience Name (Audience ID)`。

>[!NOTE]
>
>設定[!DNL Google Ad Manager]目的地時，請與您的[!DNL Google Account Manager]或Adobe代表合作，瞭解您擁有哪種帳戶型別。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出至[!DNL Google Ad Manager]目的地，請檢查您的[!DNL Google Ad Manager]帳戶。 如果成功啟用，系統會將對象填入您的帳戶。

## 疑難排解 {#troubleshooting}

如果您在使用此目的地時遇到任何錯誤，且需要聯絡Adobe或Google，請隨時保留下列ID。

這些是Adobe的Google帳戶ID：

* **[!UICONTROL 帳戶ID]**： 87933855
* **[!UICONTROL 客戶識別碼]**： 89690775