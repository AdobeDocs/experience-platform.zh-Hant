---
title: Acxiom對象分佈
description: 使用 [!DNL Acxiom Audience Distribution] 目的地以 [!DNL Acxiom's Real ID] 技術增強受眾，並啟用多個平台的受眾，例如 [!DNL Altice]、 [!DNL Ampersand]、 [!DNL Comcast]等。
badge: Beta
source-git-commit: 7db60161b638cce1845c430f6086441599a0bc61
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 6%

---


# [!DNL Acxiom Audience Distribution]目的地

>[!NOTE]
>
>[!DNL Acxiom Audience Distribution]目的地是測試版。 此目的地聯結器和檔案頁面是由[!DNL Acxiom]團隊建立和維護。 若有任何查詢或更新要求，請直接在[這裡](mailto:acxiom-adobe-help@acxiom.com)聯絡Acxiom。

使用[!DNL Acxiom Audience Distribution]目的地來增強具有[!DNL Acxiom's] [真實識別碼™](https://www.acxiom.com/real-id/real-id/)技術的對象，並啟用多個平台的對象，例如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。

本教學課程提供使用[!DNL Adobe Experience Platform]使用者介面建立[!DNL Acxiom Audience Distribution]目的地聯結器的指示。 此聯結器用於建立受眾，並將受眾發佈至選取的目的地。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Acxiom Audience Distribution]目的地，以下是[!DNL Adobe Experience Platform]客戶可以使用此聯結器解決的範例使用案例。

### 將對象從Experience Platform傳送至您的Acxiom帳戶 {#send-audiences}

如果您是行銷專業人員，想要將對象從[!DNL Experience Platform]傳送至您的[!DNL Acxiom]帳戶，以進行跨管道贏取，請使用此目的地聯結器。

例如，某個全球金融服務品牌的行銷營運部門對於透過多個廣告平台進行跨頻道客戶贏取感興趣。 他們可以使用[!DNL Acxiom Audience Distribution]目的地聯結器將對象從[!DNL Experience Platform]傳送至[!DNL Acxiom]、使用[!DNL Acxiom's Real ID]技術增強對象，以及將對象啟用至多個平台，例如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。

## 先決條件 {#prerequisites}

* **確認使用條款：**&#x200B;您必須閱讀並簽署[!DNL Acxiom's]使用條款合約，才能設定新的[!DNL Acxiom Audience Distribution]目的地。 執行銷售訂單完成後，您將會收到合約的連結。 在您簽署合約之前，您不會在Experience Platform目的地目錄中看到[!DNL Acxiom Audience Distribution]目的地卡片。 在您接受並簽署合約後，[!DNL Adobe]將完成您的上線程式，您將會看到[!DNL Acxiom Audience Distribution]目的地卡。
* **知道您的Adobe組織識別碼：**&#x200B;需要您的[!DNL Adobe]組織識別碼才能完成您的使用者合約條款。 如需如何[檢視組織ID](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)的詳細資訊，請參閱Experience Cloud *主題中的[!DNL Adobe's]*&#x200B;組織。

## 支援的目的地 {#supported-destinations}

[!DNL Acxiom Audience Distribution]目的地目前支援下列平台的對象啟用。<br>

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## 連線到目標 {#connect}

為了您的方便，系統會在幕後自動處理對[!DNL Acxiom's Audience Distribution]目的地的驗證。

## 目的地特定設定 {#destination-settings}

有些[!DNL Acxiom Audience Distribution]目的地需要其他資訊。 以下各節提供如何設定這些選項的詳細指引。

### [!DNL LG Ads] {#lg-ads}

若要設定目的地的詳細資料，請填寫下列欄位。

* **區段類別**：您的區段所屬的目標類別或垂直。 範例：金融服務、汽車、健康等。

![LG廣告目的地詳細資料](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png)

## 啟動此目標的客群 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

讀取[啟用批次設定檔匯出目的地的對象資料](/help/destinations/ui/activate-batch-profile-destinations.md)，以取得啟用此目的地對象的指示。

>[!NOTE]
>
>[!DNL Acxiom Audience Distribution]目的地僅支援完整檔案匯出。

### 對應屬性和身分 {#map}

若要讓[!DNL Acxiom Audience Distribution]目的地正確接收對象資料，您必須將來源欄位從Experience Platform對應至正確的[!DNL Acxiom Audience Distribution]目標欄位。

[!DNL Acxiom Audience Distribution]僅允許對應到以下目標欄位。 下表所述的目標欄位必須以下列順序對應。

| 欄位名稱 | 說明 | 必填 | 欄位順序 | 最大長度 |
|---|---|---|---|---|          
| 名字 | 個人的名字 | 無 | 1 | 255 |
| 靠中間 | 個人的中間名或首字母 | 無 | 2 | 50 |
| 姓氏 | 個人的姓氏 | 是 | 3 | 255 |
| 世代字尾 | 個人的尾碼 | 無 | 4 | 10 |
| 地址行1 | 主要住處的地址1欄位 | 是 | 5 | 255 |
| 地址行2 | 主要住址的地址2欄位 | 無 | 6 | 255 |
| 城市 | 主要居住地城市 | 是 | 7 | 255 |
| 狀態 | 主要居住地的州級縮寫 | 是 | 8 | 2 |
| 郵遞區號 | 主要住處的完整郵遞區號 | 是 | 9 | 10 |
| 電子郵件 | 主要電子郵件依預設，此欄位會作為重複資料刪除索引鍵，讓記錄具有唯一性 | 無 | 10 | 255 |
| 電話 | 個人的電話號碼（區碼+號碼）<br>依預設，此欄位會作為重複資料刪除索引鍵，讓記錄具有唯一性。 | 無 | 11 | 10 |

在&#x200B;**[!UICONTROL Source欄位]**&#x200B;欄位中，輸入要對應至對應目標欄位的每個來源屬性名稱，或選取箭頭圖示以開啟&#x200B;**[!UICONTROL 選取來源欄位]**&#x200B;畫面。<br>
![對應熒幕](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png)

在您對應所有欄位後，選取&#x200B;**[!UICONTROL 下一步]**。

如果您未使用[!DNL Adobe's]標準結構描述，請參閱[查詢服務UI指南](../../../query-service/ui/overview.md)檔案，以瞭解如何使用查詢服務將您的欄位名稱填入[!DNL Adobe]標準結構描述的資訊。

### 檢閱 {#review}

完成上述所有步驟後，您就有機會先檢閱目的地連線狀態和對象詳細資訊，然後再啟用（發佈）該功能。 您選取的對象將顯示在清單底部。 每個對象都會是對[!DNL Acxiom Audience Distribution] API的個別呼叫。

如果您對結果滿意，請選取&#x200B;**[!UICONTROL 完成]**&#x200B;以啟用您的目的地。

![檢閱您的對象](../../assets/catalog/advertising/acxiom-audience-distribution/review_audience.png)

## 疑難排解 {#troubleshooting}

如果目的地代表找不到您的對象，請連絡您的[!DNL Adobe]代表以尋求協助。

您需要提供下列資訊給您的[!DNL Adobe]代表：
* 客群名稱
* 目的地名稱
* 對象啟用日期
* 匯出的檔案名稱

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已成功將對象啟動至選取的目的地平台。 接下來，請聯絡您的目的地平台代表，以開始設定您的行銷活動。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)。


