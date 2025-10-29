---
title: (Beta) [!DNL Google Ad Manager 360] 連線
description: Google Ad Manager 360是Google的廣告服務平台，可讓發佈者透過視訊和行動應用程式，管理其網站上廣告的顯示方式。
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 7%

---

# (Beta) [!DNL Google Ad Manager 360]連線

>[!IMPORTANT]
>
> Google正在發佈[Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)和[Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)的變更，以支援歐盟（[歐盟使用者同意政策](https://digital-markets-act.ec.europa.eu/index_en)）中[數位市場法](https://www.google.com/about/company/user-consent-policy/) (DMA)所定義的法規遵循與同意相關需求。 自2024年3月6日起，將開始強制執行同意要求的這些變更。
> ><br/>
> >為了遵循歐盟使用者同意政策並繼續為歐洲經濟區(EEA)的使用者建立對象清單，廣告商和合作夥伴必須確保在上傳對象資料時傳遞一般使用者同意。 作為 Google 合作夥伴，Adobe 會為您提供必要的工具，以遵守歐盟之 DMA 規定的這些同意要求。
> ><br/>
> >已購買Adobe Privacy &amp; Security Shield且已設定[同意原則](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)以篩選掉非同意的設定檔的客戶，不必採取任何動作。
> ><br/>
> >未購買Adobe Privacy &amp; Security Shield的客戶必須使用[區段產生器](../../../segmentation/home.md#segment-definitions)中的[區段定義](../../../segmentation/ui/segment-builder.md)功能，篩選出未同意的設定檔，才能繼續使用現有的Real-Time CDP Google目的地而不中斷。

[!DNL Google Ad Manager 360]連線可透過[!DNL publisher provided identifiers]將[!DNL Google Ad Manager 360] (PPID)的批次上傳至[!DNL Google Cloud Storage]。

如需有關發行者提供的識別碼如何在Google Ad Manager 360中運作的詳細資訊，請參閱[Google官方檔案](https://support.google.com/admanager/answer/2880055?hl=en)。

>[!IMPORTANT]
>
>此目的地目前位於Beta，僅供有限數量的客戶使用。 若要要求存取[!DNL Google Ad Manager 360]連線，請聯絡您的Adobe代表並提供您的[!DNL organization ID]。

[!DNL Google Ad Manager 360]目的地會將[!DNL CSV]個檔案匯出至您的[!DNL Google Cloud Storage]貯體。 匯出[!DNL CSV]檔案後，您必須將其匯入您的[!DNL Google Ad Manager 360]帳戶。

## 目的地詳情 {#specifics}

請注意下列專屬於[!DNL Google Ad Manager 360]目的地的詳細資料。

* 此目的地目前不支援[隨選匯出檔案](../../ui/export-file-now.md)功能。
* 啟用的對象會在Google平台中以程式設計方式建立，並填入CSV檔案中。

## 支援的身分 {#supported-identities}

[!DNL This integration]支援下表所述的身分啟用。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | 選取此目標識別以傳送對象至[!DNL Google Ad Manager 360] |

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
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL Profile-based]** | 您正在匯出區段的所有成員，以及適用的結構描述欄位（例如您的PPID），如[目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL Batch]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

### 允許清單 {#allow-listing}

在Experience Platform中設定第一個[!DNL Google Ad Manager 360]目的地前，必須先加入允許清單。 在建立目的地之前，請務必完成下述允許清單程式。

>[!NOTE]
>
>此規則的例外狀況適用於現有[Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html)客戶。 如果您已經在Audience Manager中建立了與此Google目的地的連線，則不需要再次進行允許清單程式，您可以繼續後續步驟。

1. 依照[Google Ad Manager檔案](https://support.google.com/admanager/answer/3289669?hl=en)中所述的步驟，將Adobe新增為連結的資料管理平台(DMP)。
2. 在[!DNL Google Ad Manager]介面中，前往&#x200B;**[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]**，並啟用&#x200B;**[!UICONTROL API Access]**&#x200B;滑桿。


## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填寫必填欄位並選取&#x200B;**[!UICONTROL Connect to destination]**。

* **[!UICONTROL Access key ID]**：用於向Experience Platform驗證您的[!DNL Google Cloud Storage]帳戶的61個字元英數字串。
* **[!UICONTROL Secret access key]**：用於向Experience Platform驗證您的[!DNL Google Cloud Storage]帳戶的40個字元base64編碼字串。

如需這些值的詳細資訊，請參閱[Google雲端儲存空間HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 如需如何產生您自己的存取金鑰ID和秘密存取金鑰的步驟，請參閱[[!DNL Google Cloud Storage] 來源概觀](/help/sources/connectors/cloud-storage/google-cloud-storage.md)。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="將對象 ID 附加到對象名稱"
>abstract="選取此選項可讓這個目標中的對象名稱包含來自 Experience Platform 的對象 ID，如下所示：`Audience Name (Audience ID)`"

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL Name]**：填寫此目的地的偏好名稱。
* **[!UICONTROL Description]**：選擇性。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL Folder path]**：輸入目的地資料夾的路徑，此資料夾將裝載匯出的檔案。
* **[!UICONTROL Bucket name]**：輸入此目的地要使用的[!DNL Google Cloud Storage]儲存貯體的名稱。
* **[!UICONTROL Account ID]**：從您的[!DNL Audience Link ID]帳戶輸入您的[!DNL Google]。 這是與您的[!DNL Google Ad Manager]網路（不是您的[!DNL Network code]）相關聯的特定識別碼。 您可以在&#x200B;**[!UICONTROL Admin > Global settings]**&#x200B;介面中的[!DNL Google Ad Manager]下找到此專案。
* **[!UICONTROL Account Type]**：根據您的[!DNL Google]帳戶選取選項：
   * 對`AdX buyer`使用[!DNL Google AdX]
   * 使用`DFP by Google`作為發行者的[!DNL DoubleClick]
* **[!UICONTROL Append audience ID to audience name]**：選取此選項，讓Google Ad Manager 360中的對象名稱包含來自Experience Platform的對象識別碼，如下所示： `Audience Name (Audience ID)`。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

請參閱[啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)，以取得啟用對象至此目的地的指示。

在身分對應步驟中，您可以看到下列預先填入的對應：

| 預先填入的對應 | 說明 |
|---------|----------|
| `ECID` -> `ppid` | 這是使用者唯一可編輯的預先填入對應。 您可以從Experience Platform選取任何屬性或身分識別名稱空間，並將它們對應至`ppid`。 |
| `metadata.segment.alias` -> `list_id` | 將Experience Platform對象名稱對應至Google平台中的對象ID。 |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | 告訴Google平台何時從區段移除不符合資格的使用者。 |

[!DNL Google Ad Manager 360]需要這些對應，而且這些對應是由Adobe Experience Platform針對所有[!DNL Google Ad Manager 360]連線自動建立的。

![顯示Google Ad Manager 360對應步驟的UI影像。](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## 匯出的資料 {#exported-data}

若要驗證是否已成功匯出資料，請檢查您的[!DNL Google Cloud Storage]貯體，並確定匯出的檔案包含預期的設定檔母體。

## 疑難排解 {#troubleshooting}

如果您在使用此目的地時遇到任何錯誤，且需要聯絡Adobe或Google，請隨時保留下列ID。

這些是Adobe的Google帳戶ID：

* **[!UICONTROL Account ID]**： 87933855
* **[!UICONTROL Customer ID]**： 89690775