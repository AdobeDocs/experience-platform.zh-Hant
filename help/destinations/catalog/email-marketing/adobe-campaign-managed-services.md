---
title: Adobe Campaign Managed Cloud Services連線
description: Adobe Campaign Managed Cloud Services為跨頻道客戶體驗設計提供平台，並為視覺行銷活動的策劃、即時互動管理和跨頻道執行提供環境。
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 2%

---

# Adobe Campaign Managed Cloud Services連線 {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>此整合適用於[Adobe Campaign 8.4版或更新版本](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1)。

## 概觀 {#overview}

Adobe Campaign Managed Cloud Services為跨頻道客戶體驗設計提供平台，並為視覺行銷活動的策劃、即時互動管理和跨頻道執行提供環境。 [開始使用行銷活動](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

使用 Campaign 可以：

* 透過單一可存取的客戶檢視，推動個人化和參與。
* 將電子郵件、行動裝置、線上和線下頻道整合至客戶歷程，
* 自動化傳送有意義的即時訊息和優惠方案。

## 護欄 {#guardrails}

使用Adobe Campaign Managed Cloud Services連線時，請記得下列護欄：

* 您最多可以[啟動](#activate)25個對象到此目的地。

  您可以在Campaign檔案總管的&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 平台]** > **[!UICONTROL 選項]**&#x200B;資料夾中更新&#x200B;**NmsCdp_Aep_Audience_List_Limit**&#x200B;選項的值，以變更此限制。

* 對於每個對象，您最多可以新增20個欄位至[將](#map)對應至Adobe Campaign。

  您可以在Campaign檔案總管的&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 平台]** > **[!UICONTROL 選項]**&#x200B;資料夾中更新&#x200B;**NmsCdp_Aep_Destinations_Max_Columns**&#x200B;選項的值，以變更此限制。

* Azure Blob儲存資料登陸區域(DLZ)上的資料保留：7天。
* 啟用頻率為最少3小時。
* 此連線支援的檔案名稱長度上限為255個字元。 當您[設定匯出的檔案名稱](../../ui/activate-batch-profile-destinations.md#configure-file-names)時，請確定檔案名稱不超過255個字元。 超過檔案名稱長度上限會導致啟用錯誤。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用Adobe Campaign管理服務目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

* Adobe Experience Platform會建立客戶設定檔，其中納入身分圖表、來自analytics的行為資料、合併離線和線上資料等資訊。 透過這項整合，您可以透過Adobe Experience Platform支援的受眾來增強Adobe Campaign中已存在的細分功能，並且因此可以在Campaign中啟用該資料。

  例如，一家運動服裝公司想要運用Adobe Experience Platform支援的對象，並使用Adobe Campaign啟用他們，以便透過Adobe Campaign支援的不同管道聯絡其客戶基礎。 傳送訊息後，他們想要使用Adobe Campaign的體驗資料（例如傳送、開啟和點按）增強Adobe Experience Platform中的客戶設定檔。

  跨通路的行銷活動在整個Adobe Experience Cloud生態系統中更為一致，並擁有豐富的客戶個人檔案，可快速適應和學習。


* 除了在Campaign中啟用對象外，您還可以運用Adobe Campaign Managed Services目的地來引進其他設定檔屬性，這些屬性會繫結至Adobe Experience Platform上的設定檔，並設定同步程式，以便在Adobe Campaign資料庫中更新。

  例如，假設您擷取Adobe Experience Platform中的選擇加入和選擇退出值。 透過此連線，您可以將這些值帶入Adobe Campaign並建立同步程式，以便定期更新。

  >[!NOTE]
  >
  >Adobe Campaign資料庫中已存在的設定檔可使用「設定檔屬性同步」。

[進一步瞭解Adobe Campaign與Adobe Experience Platform的整合](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)

## 支援的身分 {#supported-identities}

*Adobe Campaign Managed Cloud Services*&#x200B;支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| external_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，請選取此目標身分。 我們建議使用此身分識別，並將其對應至您的Campaign執行個體中代表客戶的ID (loyalty_ID、account_ID、customer_ID...) |
| ECID | Experience Cloud ID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 如需詳細資訊，請參閱[ECID](/help/identity-service/features/ecid.md)上的下列檔案。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform同時支援純文字和SHA256雜湊電話號碼。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| GAID | GOOGLE ADVERTISING ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出對象的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 選取執行個體]**：您的&#x200B;**[!DNL Campaign]**&#x200B;行銷執行個體。
* **[!UICONTROL 目標對應]**：選取您在&#x200B;**[!DNL Adobe Campaign]**&#x200B;中使用的目標對應，以傳送傳遞。 [了解更多](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html)。
* **[!UICONTROL 選取同步型別]**：

   * **[!UICONTROL 對象同步]**：使用此選項將Adobe Experience Platform對象傳送到Adobe Campaign。
   * **[!UICONTROL 設定檔同步（僅更新）]**：使用此選項將Adobe Experience Platform設定檔屬性帶入Adobe Campaign，並建立同步程式，以便定期更新。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

### 治理原則與執行動作 {#governance}

選取適用於您要匯出至目的地之資料的行銷動作。 若為Adobe Campaign，建議您選取&#x200B;**[!UICONTROL 電子郵件鎖定目標]**&#x200B;行銷動作。

如需行銷動作的詳細資訊，請參閱[資料使用原則概觀](/help/data-governance/policies/overview.md)頁面。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

讀取[啟用批次設定檔匯出目的地的對象資料](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html)，以取得啟用此目的地的對象資料的相關指示。

### 對應屬性和身分 {#map}

選取要與設定檔一起匯出的XDM欄位，並將它們對應到相對應的Adobe Campaign欄位。[進一步瞭解電子郵件行銷目的地的身分和屬性選擇](overview.md)

1. 選取來源欄位：

   * 選取&#x200B;**識別碼** （例如：電子郵件欄位）作為在Adobe Experience Platform和Adobe Campaign中唯一識別設定檔的來源識別碼。

   * 選取需要匯出至Adobe Campaign的所有其他&#x200B;**XDM來源設定檔屬性**。

   >[!NOTE]
   >
   >「segmentMembershipStatus」欄位是反映segmentMembership狀態的必要對應。 此欄位預設為新增，無法修改或移除。

1. 在Adobe Campaign中將每個欄位與其目標欄位對應。 可用的目標欄位由[建立目的地](#destination-details)時選取的目標對應決定。

1. 識別強制屬性和重複資料刪除索引鍵。 請注意，標示為「必要」或「重複資料刪除索引鍵」的屬性中的值不可以是Null。

   * [必要屬性](../../ui/activate-batch-profile-destinations.md#mandatory-attributes)確定所有設定檔記錄都包含選取的屬性。 例如：所有匯出的設定檔都包含電子郵件地址。 建議將身分欄位和用作重複資料刪除索引鍵的欄位都設為強制性。
   * [重複資料刪除索引鍵](../../ui/activate-batch-profile-destinations.md#mandatory-attributes)是決定使用者要為其設定檔進行重複資料刪除之身分的主索引鍵。

     >[!IMPORTANT]
     >
     >請確定重複資料刪除索引鍵屬性的名稱符合所選目標對應的欄名稱。

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. 執行對應後，您可以檢閱並完成目的地設定，以開始傳送資料給&#x200B;**[!DNL Campaign]**。
   [瞭解如何檢閱並完成目的地設定](/help/destinations/destination-types.md#review)。

## 匯出的資料/驗證資料匯出 {#exported-data}

一旦啟用目的地後，您就可以在Campaign中存取對應的工作和匯出的資料。

### 監視資料匯出作業 {#jobs}

導覽至&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 稽核]** > **[!UICONTROL 對象載入工作]**&#x200B;功能表，以監視從Adobe Experience Platform啟用的所有匯出工作。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### 存取匯出的資料 {#data}

若為&#x200B;**[!UICONTROL 對象同步]**，您可以導覽至&#x200B;**[!UICONTROL 設定檔及目標]** > **[!UICONTROL 清單]** > **[!UICONTROL AEP對象]**&#x200B;功能表，以檢查匯出的對象。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

針對&#x200B;**[!UICONTROL 設定檔同步（僅更新）]**，資料會自動更新至目的地中啟用的對象所定位之每個設定檔的Campaign資料庫。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。
