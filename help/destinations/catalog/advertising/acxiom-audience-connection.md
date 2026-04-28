---
title: Acxiom對象連線
description: 使用 [!DNL Acxiom Audience Connection] 目的地來增強使用 [!DNL Acxiom]'s [!DNL Real ID] 技術的對象，並跨廣告平台啟用這些對象。
source-git-commit: 71e655be2bdae3c89bd1652e2f83ab7bcc8c18fa
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 7%

---


# [!DNL Acxiom Audience Connection]目標

使用[!DNL Acxiom Audience Connection]目的地，以[!DNL Acxiom]的[真實識別碼™](https://www.acxiom.com/real-id/real-id/)技術增強對象。 然後跨平台啟用這些對象，例如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。

>[!NOTE]
>
>此目的地聯結器和檔案頁面是由[!DNL Acxiom]團隊建立和維護。 若有任何查詢或更新要求，請直接透過[acxiom-adobe-help@acxiom.com](mailto:acxiom-adobe-help@acxiom.com)聯絡[!DNL Acxiom]。

請依照下列步驟，使用[!DNL Adobe Experience Platform]使用者介面建立[!DNL Acxiom Audience Connection]目的地聯結器。 使用此聯結器來建立受眾，並將受眾發佈到所選的目的地。

## 使用案例 {#use-cases}

下列使用案例顯示如何使用[!DNL Acxiom Audience Connection]目的地。

### 將對象從[!DNL Experience Platform]傳送至您的[!DNL Acxiom]帳戶 {#send-audiences}

使用此目的地聯結器將對象從[!DNL Experience Platform]傳送至您的[!DNL Acxiom]帳戶，以進行跨管道贏取。

例如，某個全球金融服務品牌的行銷營運部門對於透過多個廣告平台進行跨頻道客戶贏取感興趣。 他們可以使用[!DNL Acxiom Audience Connection]目的地聯結器將對象從[!DNL Experience Platform]傳送至[!DNL Acxiom]、使用[!DNL Acxiom]的[!DNL Real ID]技術增強對象，以及將對象啟用至多個平台，例如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。

## 先決條件 {#prerequisites}

設定[!DNL Acxiom Audience Connection]目的地之前，請先完成下列必要條件。

* **確認使用條款：**&#x200B;閱讀並簽署[!DNL Acxiom]的使用條款合約。 執行銷售訂單完成後，您會收到協定的連結。 在您簽署合約之前，[!DNL Acxiom Audience Connection]目的地卡片不會出現在[!DNL Experience Platform]目的地目錄中。 在您接受並簽署合約之後，[!DNL Adobe]會完成您的設定，且[!DNL Acxiom Audience Connection]目的地卡片會顯示。
* **知道您的[!DNL Adobe]組織識別碼：**&#x200B;需要您的[!DNL Adobe]組織識別碼才能完成您的使用條款合約。 如需如何[檢視組織ID](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)的詳細資訊，請參閱[!DNL Adobe]在Experience Cloud中的&#x200B;*組織*&#x200B;主題。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | 是 | 透過[!DNL Experience Platform] [細分服務](/help/segmentation/home.md)產生的對象。 |
| 所有其他受眾來源 | 是 | 此類別包含透過[!DNL Segmentation Service]產生的對象以外的所有對象來源。 閱讀[各種對象來源](/help/segmentation/ui/audience-portal.md#customize)。 部分範例包括： <ul><li>自訂上傳對象[從CSV檔案匯入](/help/segmentation/ui/audience-portal.md#import-audience)至[!DNL Experience Platform]，</li><li>相似受眾，</li><li>同盟對象，</li><li>在其他[!DNL Experience Platform]應用程式（例如[!DNL Adobe Journey Optimizer]）中產生的對象</li><li>及更多內容。</li></ul> |

{style="table-layout:auto"}

### 依資料型別區分的支援對象 {#supported-audiences-data-type}

下表說明您可以將哪些對象資料型別匯出至此目的地。

| 對象資料型別 | 支援 | 說明 | 使用案例 |
| -------------------- | ----------- | ------------- | ----------- |
| [人員對象](/help/segmentation/types/people-audiences.md) | 是 | 根據客戶設定檔。 使用這些功能來針對特定人群進行行銷活動。 | 經常購買者、購物車放棄者 |
| [帳戶對象](/help/segmentation/types/account-audiences.md) | 無 | 針對帳戶型行銷策略，鎖定特定組織內的個人。 | B2B行銷 |
| [潛在客戶對象](/help/segmentation/types/prospect-audiences.md) | 無 | 將目標定位為尚未成為客戶但與目標受眾具有相同特性的個人。 | 使用第三方資料進行勘探 |
| [資料集匯出](/help/catalog/datasets/overview.md) | 無 | 儲存在[!DNL Adobe Experience Platform]資料湖中的結構化資料集合。 | 報告、資料科學工作流程 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

下表說明目的地匯出型別和頻率。

| 項目 | 類型 | 附註 |
| ---- | ---- | ----- |
| 匯出類型 | **[!UICONTROL Audience export]** | 匯出具有[!DNL Acxiom Audience Connection]目的地中所使用識別碼（名稱、電話號碼或其他）的對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL Batch]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 支援的目的地 {#supported-destinations}

透過[!DNL Acxiom Audience Connection]目的地啟用下列平台的對象。

* [!DNL Altice]
* [[!DNL Amazon]](#amazon)
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL Facebook]](#facebook)
* [[!DNL LG Ads]](#lg-ads)
* [[!DNL Pinterest]](#pinterest)
* [!DNL Spectrum]
* [!DNL Viant]
* [[!DNL Vizio]](#vizio)

## 連線到目標 {#connect}

[!DNL Experience Platform]會自動處理您[!DNL Acxiom Audience Connection]目的地的驗證。

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

## 目的地特定設定 {#destination-settings}

有些[!DNL Acxiom Audience Connection]目的地需要其他資訊。 以下章節提供如何設定這些選項的詳細指引。

### [!DNL Amazon] {#amazon}

若要設定目的地的詳細資訊，請完成下列欄位。

* **[!UICONTROL Publisher Account ID]**：輸入與此目的地關聯的發行者帳戶識別碼。

  ![&#x200B; [!DNL Amazon]目的地詳細資料面板的熒幕擷取畫面顯示[發行者帳戶ID]欄位。](../../assets/catalog/advertising/acxiom-audience-distribution/amazon_destination_details.png){zoomable="yes"}

### [!DNL Facebook] {#facebook}

若要設定目的地的詳細資訊，請完成下列欄位。

* **[!UICONTROL Destination Account ID]**：輸入此目的地的目的地帳戶識別碼。

  ![顯示[目的地帳戶ID]欄位的[!DNL Facebook]目的地詳細資料面板的熒幕擷圖。](../../assets/catalog/advertising/acxiom-audience-distribution/facebook_destination_details.png){zoomable="yes"}

### [!DNL LG Ads] {#lg-ads}

若要設定目的地的詳細資訊，請完成下列欄位。

* **[!UICONTROL Segment Category]**：您的區段所屬的目標類別或垂直。 範例：金融服務、汽車或健康。

  ![顯示[區段類別]欄位的[!DNL LG Ads]目的地詳細資料面板的熒幕擷圖。](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png){zoomable="yes"}

### [!DNL Pinterest] {#pinterest}

若要設定目的地的詳細資訊，請完成下列欄位。

* **[!UICONTROL Destination Account ID]**：輸入此目的地的目的地帳戶識別碼。

  ![顯示[目的地帳戶ID]欄位的[!DNL Pinterest]目的地詳細資料面板的熒幕擷圖。](../../assets/catalog/advertising/acxiom-audience-distribution/pinterest_destination_details.png){zoomable="yes"}

### [!DNL Vizio] {#vizio}

若要設定目的地的詳細資訊，請完成下列欄位。

* **[!UICONTROL Advertiser Name]**：輸入此目的地的廣告商名稱。

  ![顯示[廣告商名稱]欄位的[!DNL Vizio]目的地詳細資料面板的熒幕擷圖。](../../assets/catalog/advertising/acxiom-audience-distribution/vizio_destination_details.png){zoomable="yes"}

## 啟動此目標的對象 {#activate}

讀取[啟用批次設定檔匯出目的地的對象資料](/help/destinations/ui/activate-batch-profile-destinations.md)，以取得啟用此目的地對象的指示。

>[!IMPORTANT]
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png){width="100" zoomable="yes"}

>[!NOTE]
>
>[!DNL Acxiom Audience Connection]目的地僅支援完整檔案匯出。

### 對應屬性和身分 {#map}

若要正確接收對象資料，請將來源欄位從[!DNL Experience Platform]對應到正確的[!DNL Acxiom Audience Connection]目標欄位。

下列目標欄位會以[!DNL Acxiom]要求的順序自動預先填入。 您必須將來源欄位對應到每個目標欄位，才能完成啟動流程。

>[!IMPORTANT]
>
>所有目標欄位都需要在UI中完成對應。 不過，只有&#x200B;**[!UICONTROL Last Name]**、**[!UICONTROL Address Line 1]**、**[!UICONTROL City]**、**[!UICONTROL State]**&#x200B;和&#x200B;**[!UICONTROL Zip Code]**&#x200B;需要在您的設定檔結構描述中取得實際資料。 將任何可用的來源欄位對應到剩餘的目標欄位以滿足UI需求。

| 欄位名稱 | 說明 | UI所需 | 處理所需的資料 | 欄位順序 | 最大長度 |
| -------------------- | ------------ | ------------------ | ---------------------------- | ----------- | ---------- |
| 名字 | 個人的名字 | 是 | 無 | 1 | 255 |
| 靠中間 | 個人的中間名或首字母 | 是 | 無 | 2 | 50 |
| 姓氏 | 個人的姓氏 | 是 | **是** | 3 | 255 |
| 世代字尾 | 個人的尾碼 | 是 | 無 | 4 | 10 |
| 地址行1 | 主要住處的地址1欄位 | 是 | **是** | 5 | 255 |
| 地址行2 | 主要住址的地址2欄位 | 是 | 無 | 6 | 255 |
| 城市 | 主要居住地城市 | 是 | **是** | 7 | 255 |
| 狀態 | 主要居住地的州級縮寫 | 是 | **是** | 8 | 2 |
| 郵遞區號 | 主要住處的完整郵遞區號 | 是 | **是** | 9 | 10 |
| 電子郵件 | 主要電子郵件。 依預設，此欄位會作為重複資料刪除索引鍵，讓記錄具有唯一性。 | 是 | 無 | 10 | 255 |
| 電話 | 個人的電話號碼（區碼+號碼）。 依預設，此欄位會作為重複資料刪除索引鍵，讓記錄具有唯一性。 | 是 | 無 | 11 | 10 |

{style="table-layout:auto"}

在&#x200B;**[!UICONTROL Source Field]**&#x200B;欄位中，輸入要對應至對應目標欄位的每個來源屬性名稱。 或選取&#x200B;**[!UICONTROL Select source field]**&#x200B;以瀏覽可用的來源欄位。

![對應畫面顯示來源欄位和目標欄位，其中的[!DNL Acxiom]必要欄位已預先填入[!DNL Acxiom Audience Connection]目的地。](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png){zoomable="yes"}

對應所有欄位後，選取&#x200B;**[!UICONTROL Next]**。

若要使用非標準結構描述，請參閱[查詢服務UI指南](/help/query-service/ui/overview.md)，將您的欄位名稱對應到[!DNL Adobe]標準結構描述。

### 檢閱您的目的地 {#review}

完成所有步驟後，請先檢閱目的地連線狀態和對象詳細資訊，再加以啟用。 您選取的對象會出現在清單中。 每個對象都是對[!DNL Acxiom Audience Connection] API的個別呼叫。

如果您對結果滿意，請選取&#x200B;**[!UICONTROL Finish]**&#x200B;以啟用您的目的地。

![檢閱您的對象畫面，顯示目的地連線狀態和選取的對象。](../../assets/catalog/advertising/acxiom-audience-distribution/review_audience.png){zoomable="yes"}

## 疑難排解 {#troubleshooting}

如果目的地代表找不到您的對象，請連絡您的[!DNL Adobe]代表以尋求協助。

提供下列資訊給您的[!DNL Adobe]代表：

* 客群名稱
* 目的地名稱
* 對象啟用日期
* 匯出的檔案名稱

## 後續步驟 {#next-steps}

您已成功將對象啟動至選取的目的地平台。 接下來，請聯絡您的目的地平台代表，以開始設定您的行銷活動。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。
